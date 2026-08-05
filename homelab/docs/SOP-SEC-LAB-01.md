---
Document ID: SOP-SEC-LAB-01
Version: 1.0.0 (Baseline Sandbox)
Last Updated: August 2026
Status: Active / Approved
---

## ─── [ SECTION 1: ARCHITECTURAL OVERVIEW ] ───

Standard containerization models (e.g., Docker) fail to mitigate kernel-level exploitation because they share the underlying host operating system kernel. Triggering a kernel panic or memory corruption vulnerability inside a standard container will destabilize the entire physical machine.

To achieve true isolation, this architecture implements a strict **Defense-in-Depth** model:

```text
[ PHYSICAL KALI HOST ] ──(No Virtual Bridge)──> [ BOUNDARY OF ABSOLUTE ISOLATION ]
                                                              │
    ┌─────────────────────── KVM VIRTUAL ISOLATED SWITCH ─────┴───────────────────────┐
    │                                             │                                   │
    ▼                                             ▼                                   ▼
[ MODULE 1: ATTACK ]                    [ MODULE 2: GATEWAY ]               [ MODULE 3: TARGETS ]
Ubuntu VM (Raw Packets)                 Rocky Linux (Router)                Nested Container Node
   - Python / Rust Tooling                 - Logs State Interactions           - Vulnerable Kernel
   - Fixed Test IPs                        - IP/IPv6 Forwarding Core           - Windows Server Instance
```

1. **Hardware-Level Isolation (The Hypervisor):** KVM/QEMU uses physical CPU extensions (Intel VT-x / AMD-V) to segment memory space completely away from the host Kali system.
2. **Software-Defined Air-Gapping (The Network Layer):** All physical network interfaces (Wi-Fi/Ethernet) are decoupled from the testing environment. Virtual nodes communicate exclusively via an isolated host-memory switch.
3. **Modular Ephemerality (The Storage Layer):** Target systems are deployed as lightweight, linked clones from a locked, immutable "Golden Base" image, allowing instant disposal and recovery upon a system crash.

---

## ─── [ SECTION 2: NETWORK ISOLATION PROTOCOLS ] ───

### Step 1: Purging the Default NAT Bridge
By default, KVM initializes a shared network bridge (`virbr0`) that routes virtual machines to the public internet. This interface must be systematically disabled to prevent accidental outbound exploit traffic.

```bash
# Stop the default internet-connected virtual network
sudo virsh net-destroy default

# Disable the default network from starting automatically on boot
sudo virsh net-autostart --disable default
```

### Step 2: Provisioning the Isolated Virtual Switch
Define a strict, host-isolated network fabric. This network configuration assigns IP ranges but deliberately omits any `<forward>` tags or gateway routes to the host.

1. Create a local configuration file named `isolated-network.xml`:
```xml
<network>
  <name>isolated-airgap</name>
  <bridge name='virbr1' stp='on' delay='0'/>
  <domain name='lab.local'/>
  <ip address='10.10.10.1' netmask='255.255.255.0'>
    <dhcp>
      <range start='10.10.10.10' end='10.10.10.50'/>
    </dhcp>
  </ip>
</network>
```

2. Commit, define, and activate the isolated boundary:
```bash
# Define the network from the XML blueprint
sudo virsh net-define isolated-network.xml

# Activate the isolated host switch
sudo virsh net-start isolated-airgap

# Configure the network to persist across host reboots
sudo virsh net-autostart isolated-airgap
```

---

## ─── [ SECTION 3: STORAGE MODULARITY & RECOVERY ] ───

To maintain high testing momentum, researchers must assume that target systems will continuously be destroyed or corrupted by experimental code. Utilizing QCOW2 backing chains removes the overhead of repeatedly reinstalling operating systems.

### Step 1: Establishing the Immutable "Golden Base"
1. Install a clean, minimalist instance of `Ubuntu Server` or `Rocky Linux` via KVM.
2. Update packages, configure base dependencies (e.g., Python, Rust, Git, Build Essentials), and shut down the machine.
3. Lock the raw storage volume (`golden-base.qcow2`) as a read-only master file.

### Step 2: Deploying a Disposable Linked Target Module
When initializing a new round of protocol or kernel fuzzing, generate an ephemeral delta disk that references the master file.

```bash
# Create a hyper-lightweight linked clone disk image
qemu-img create -f qcow2 -b /var/lib/libvirt/images/golden-base.qcow2 /var/lib/libvirt/images/target-module-01.qcow2
```
*Note: The resulting `target-module-01.qcow2` file consumes virtually zero initial disk space, reading data directly from the baseline image while writing any state modifications or crash dumps to its localized layer.*

### Step 3: Rapid Recovery Post-Kernel Panic
When an experimental packet triggers an unrecoverable kernel panic or state corruption on the target node, execute a hot-swap recovery routine:

```bash
# Forcefully tear down the crashed or corrupted node
virsh destroy target-node-01

# Wipe the corrupted delta disk image completely
rm /var/lib/libvirt/images/target-module-01.qcow2

# Instantly provision a fresh, clean delta disk from the Golden Base
qemu-img create -f qcow2 -b /var/lib/libvirt/images/golden-base.qcow2 /var/lib/libvirt/images/target-module-01.qcow2

# Boot the node back into an pristine testing state (Time Elapsed: < 5 seconds)
virsh start target-node-01
```

---

## ─── [ SECTION 4: POST-DEPLOYMENT VERIFICATION ] ───

Before executing any custom packet-crafting or state-exhaustion scripts, researchers must validate containment via a dual-point audit:

1. **The Outbound Leak Test:** From inside a running laboratory node (`target-node-01`), execute an outbound ping to an external public address (e.g., `ping 8.8.8.8`). The operation **must** result in a permanent network timeout error.
2. **The Host Isolation Test:** Run a network packet capture utility on the physical host machine's interfaces (`sudo tcpdump -i any icmp`). Send testing packets within the lab. The traffic **must** remain entirely invisible to the physical host's network interfaces, proving complete encapsulation inside the memory-mapped virtual switch.
