# Standard Operating Procedure (SOP): Hardening the Physical Host System for Low-Level Hypervisor Research

**Document ID:** SOP-SEC-HOST-01  
**Classification:** Public / Defensive Research Community  
**Objective:** To systematically harden a physical Kali Linux host machine running a KVM/QEMU hypervisor, establishing absolute network containment and process isolation to prevent guest VM breakout, kernel panic spillover, or traffic leakage.

---

## SECTION 1: ARCHITECTURAL OVERVIEW

Establishing a software-defined air-gapped network switch inside a hypervisor is only half the isolation battle. By default, the underlying Linux host kernel acts as a helpful, adaptive routing engine. If an experimental packet-crafting tool triggers a routing loop or a memory exploit within the guest sandbox, the host operating system may attempt to intercept, process, or automatically route that traffic.

To seal the isolation boundary completely, this procedure enforces **Four Host Defenses**:

1. **Network Layer De-configuration (The Leak Shield):** Disabling global IP forwarding and network visibility to blindfold the host from lab traffic.
2. **Mandatory Access Control (The Sandbox Shield):** Utilizing AppArmor to strictly confine QEMU processes to restricted memory and storage zones.
3. **Local Firewall Enforcement (The Traffic Shield):** Deploying Netfilter/UFW rules to explicitly drop any inbound connections attempting to pivot from the lab subnet to the host.
4. **Storage Exhaustion Mitigation (The Crash Shield):** Structuring isolated storage allocation to prevent runaway guest crash logs from freezing the physical system.

---

## SECTION 2: NETWORK LAYER DE-CONFIGURATION

### Step 1: Disabling Global Packet Forwarding
By default, the Linux kernel may attempt to act as a router. We must ensure the physical host explicitly drops any packets attempting to jump between the virtual lab networks and the host's actual internet connection (Wi-Fi/Ethernet).

1. Execute the runtime commands to immediately kill IP forwarding:
```bash
sudo sysctl -w net.ipv4.ip_forward=0
sudo sysctl -w net.ipv6.conf.all.forwarding=0
```

2. Persist these configuration parameters across system reboots by appending them to a dedicated kernel hardening profile:
```bash
echo "net.ipv4.ip_forward=0" | sudo tee -a /etc/sysctl.d/99-security-hardening.conf
echo "net.ipv6.conf.all.forwarding=0" | sudo tee -a /etc/sysctl.d/99-security-hardening.conf
```

### Step 2: Blindfolding the Host from the Virtual Bridge (`virbr1`)
When KVM instantiates an isolated bridge interface, the host kernel creates a local virtual adapter pointing inside that network. To prevent the host from interacting with lab traffic, ARP and Neighbor Discovery responses must be restricted on that interface.

1. Inject interface-specific constraints into the kernel control layout (replace `virbr1` if your isolated lab network uses a different index name):
```bash
echo "net.ipv4.conf.virbr1.arp_ignore=1" | sudo tee -a /etc/sysctl.d/99-security-hardening.conf
echo "net.ipv4.conf.virbr1.arp_announce=2" | sudo tee -a /etc/sysctl.d/99-security-hardening.conf
```

2. Force the host kernel to reload and apply all newly added security configuration layers:
```bash
sudo sysctl --system
```

---

## SECTION 3: HYPERVISOR PROCESS ISOLATION

If an experimental script triggers a radical memory corruption event inside a guest virtual machine, the virtualization layer must be restricted so that the rogue VM cannot escalate privileges or read file paths on the physical Kali Linux machine.

### Step 1: Enforcing AppArmor Confinement
AppArmor provides Mandatory Access Control (MAC) to ensure that the QEMU driver process can only read and write files within its designated, secure virtual disk directories.

1. Open the primary QEMU hypervisor driver configuration profile:
```bash
sudo nano /etc/libvirt/qemu.conf
```

2. Locate the `security_driver` directive. Uncomment the line and explicitly enforce `apparmor`:
```text
security_driver = "apparmor"
```

3. Save the file, exit the editor, and restart the virtualization infrastructure management daemon to bind the active security policies:
```bash
sudo systemctl restart libvirtd
```

---

## SECTION 4: TRAFFIC AND STORAGE CONTAINMENT

### Step 1: Defending Administrative Ports via Host Firewall
Isolated target nodes must never be allowed to talk back to your physical computer's internal ports (such as SSH, database ports, or VNC listeners). We establish a strict block policy filtering out traffic originating from the lab subnet (`10.10.10.0/24`).

1. Enable the Uncomplicated Firewall (UFW) baseline:
```bash
sudo ufw enable
```

2. Establish the drop policy targeting the entire lab network segment:
```bash
sudo ufw deny from 10.10.10.0/24 to any
```

3. Audit the firewall state to ensure the drop rule is cleanly registered at the top of the stack:
```bash
sudo ufw status verbose
```

### Step 2: Storage Quota Allocation
When executing high-risk protocol or kernel fuzzing scripts, a guest virtual machine crashing via a kernel panic may generate massive logs or storage core dumps. If virtual disks are set to grow infinitely (dynamic allocation without cap), a runaway log loop can fill the physical system storage disk entirely, locking the researcher out of the host machine.

* **Operational Mandate:** All virtual storage files (`.qcow2`) assigned to target nodes must have a strict, maximum size threshold (e.g., hard cap at 20GB limits) allocated during the provisioning phase. 
* Monitor storage usage metrics periodically from the host terminal to ensure disk health:
```bash
df -h
```

---

## SECTION 5: COMPREHENSIVE RECOVERY & AUDIT

Once host hardening steps are complete, execute a diagnostic loop to verify containment:

1. **The Inbound Block Audit:** Boot an isolated lab node, open a terminal inside the guest, and attempt to run a port scan against the host gateway address (e.g., `nmap 10.10.10.1`). The request **must** be dropped silently by the host firewall.
2. **The AppArmor Status Check:** Run `sudo aa-status` on the physical Kali host. Verify that all active `libvirt` and `qemu` execution processes are explicitly listed under **enforce mode**, proving the hardware sandbox layer is strictly constrained.
