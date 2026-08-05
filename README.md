# The Architecture of Progression: A Constraint-Driven Engineering Roadmap

Welcome to my central portfolio. This repository documents a structured, multi-phase engineering journey spanning from the metal to the cosmos. What begins as deep exploration into low-level systems programming, operating system internals, and offensive security tooling evolves systematically into planet-scale distributed networks, adversarial machine learning, and space-edge communication architectures. Designed to demonstrate elite, constraint-driven engineering and uncompromising software reliability, this comprehensive curriculum tracks the development of highly optimized infrastructure capable of delivering profound societal value—whether securing critical systems on Earth or routing data through the stars.

---

## Engineering Pillars & Core Competencies

| Systems & Kernel | Distributed & Network Scale | Space-Edge & Resiliency | Security & Intelligence |
| :--- | :--- | :--- | :--- |
| • C / Rust / Assembly | • P2P Architecture (DHT) | • Delay-Tolerant Net. (DTN) | • Offensive Tooling Dev |
| • OS Internals / Drivers | • Stateless Network Scanning | • CubeSat Flight Software | • Binary Exploitation |
| • Memory Management | • Custom Edge Routing (BGP) | • Wasm Runtime Isolation | • Process Injection |
| • Constraint Optimization | • Zero-Copy Data Ingestion | • Astrodynamics Cryptography | • Adversarial ML / Evasion |
| • Linux Kernel Modules | • Ephemeral Cloud Workers | • Space-Grade Protocols | • Sub-System Auditing |

---

## The Hardware-Constrained Engineering Principle
This entire infrastructure framework is intentionally engineered, benchmarked, and validated on a single **Dell OptiPlex 3040 (Intel i5 CPU, 16GB RAM, 500GB HDD)** purchased as an unprovisioned, non-bootable bare-metal unit and independently restored via custom BIOS/firmware configuration and low-level storage provisioning.

* **The Philosophy:** Global scale should not require infinite cloud budgets. If an adversarial nation-state threat actor or independent researcher can orchestrate sophisticated attacks using a $100 consumer-grade workstation, defensive engineers must learn to audit, detect, and mitigate those threats with the exact same resource efficiency.
* **The Engineering Constraint:** By utilizing zero-copy data ingestion pipelines, lightweight OS containerization topologies (LXC, Containerlab), and low-footprint custom runtimes, this framework achieves planetary threat simulation and space-edge resiliency testing without saturating host memory or causing disk I/O bottlenecks. 

---

## Repository Architecture

```text
├── 01_The_Core/                      # (Phases 1-3) Local Systems & Kernel Architecture
│   ├── Phase_01_Hardware_Assembly/
│   ├── Phase_02_Systems_Networking/
│   └── Phase_03_Operating_Systems/
│
├── 02_The_Shell/                     # (Phases 4-7) Security Engineering & Malware Primitives
│   ├── Phase_04_Telemetry_RE/
│   ├── Phase_05_Adversary_Simulation/
│   ├── Phase_06_Infrastructure_Automation/
│   └── Phase_07_AI_Offensive_Tooling/
│
├── 03_The_Mesh/                      # (Phases 8-10) Adversarial AI & Enterprise Orchestration
│   ├── Phase_08_Adversarial_ML/
│   ├── Phase_09_Enterprise_DevSecOps/
│   └── Phase_10_Telemetry_Forensics/
│
└── 04_The_Global_Cosmic_Fabric/      # (Phases 11-13) Internet Systems & Space Communications
    ├── Phase_11_Distributed_Systems/
    ├── Phase_12_Planetary_Operations/
    └── Phase_13_Orbital_Infrastructure/
```

---

### The Laboratory
Before running any scripts in the `simulations/` directory, you must establish a secure, host-isolated workspace. 
* [ ] Review the Laboratory Architecture Blueprint in [homelab/README.md](./homelab/README.md)
* [ ] Provision the Sandbox via [SOP-SEC-LAB-01](./homelab/docs/SOP-SEC-LAB-01.md)

---

## Project Index & Progress Tracking

### Phase 1: Hardware, Architecture, & Assembly
*   [x] **Project 1: Base64 Encoder/Decoder** | https://github.com/ryan-sharpnack/asm-base64-codec
*   [x] **Project 2: 4-Bit ALU Simulator** | https://github.com/ryan-sharpnack/alu-4bit-simulator
*   [x] **Project 3: CPU Register State Dumper** | https://github.com/ryan-sharpnack/asm-register-dumper

### Phase 2: Core Systems Engineering & Networking
*   [x] **Project 4: Hex Dump Utility** | https://github.com/ryan-sharpnack/hex-dump-utility
*   [x] **Project 5: Raw TCP Port Scanner** | https://github.com/ryan-sharpnack/raw-tcp-port-scanner
*   [x] **Project 6: Custom malloc Allocator** | https://github.com/ryan-sharpnack/custom-malloc-allocator

### Phase 3: Operating System Mastery
*   [x] **Project 7: Windows PE Header Parser** | https://github.com/ryan-sharpnack/pe-header-parser
*   [x] **Project 8: Linux ELF Symbol Analyzer** | https://github.com/ryan-sharpnack/elf-dependency-analyzer
*   [x] **Project 9: Linux strace Prototype** | https://github.com/ryan-sharpnack/ptrace-syscall-tracer

### Phase 4: Telemetry & Defensive Reverse Engineering
*   [ ] **Project 10: Process Memory Scanner** | Status: Planned
*   [ ] **Project 11: Static Threat Scoring Engine** | Status: Planned
*   [ ] **Project 12: Kernel Event Log Parser** | Status: Planned

### Phase 5: Adversary Simulation & Evasion
*   [ ] **Project 13: Windows DLL Injector** | Status: Planned
*   [ ] **Project 14: Compile-Time API Hasher** | Status: Planned
*   [ ] **Project 15: Sandbox Evasion Fingerprinter** | Status: Planned

### Phase 6: Infrastructure & Automation
*   [ ] **Project 16: Threaded Reverse Shell Payload** | Status: Planned
*   [ ] **Project 17: Concurrent Go C2 Listener** | Status: Planned
*   [ ] **Project 18: Encrypted Custom Data Stager** | Status: Planned

### Phase 7: AI-Driven Offensive Tooling & Malware
*   [ ] **Project 19: AI-Driven Evasive Shellcode Generator** | Status: Planned
*   [ ] **Project 20: Intelligent EDR-Aware Context Fingerprinter** | Status: Planned
*   [ ] **Project 21: Autonomous Phishing & C2 Orchestration Engine** | Status: Planned

### Phase 8: Attacking AI Infrastructure & Models (Adversarial ML)
*   [ ] **Project 22: Local LLM Jailbreak & Prompt Injection Harness** | Status: Planned
*   [ ] **Project 23: Live Process Memory Model Inversion Attack** | Status: Planned
*   [ ] **Project 24: Direct-on-Disk ML Model Poisoning Script** | Status: Planned

### Phase 9: Enterprise DevSecOps, Cloud Evasion, & Infrastructure Exploitation
*   [ ] **Project 25: GitOps Ransomware & Infrastructure Destroyer Simulation Pipeline** | Status: Planned
*   [ ] **Project 26: Cloud-Native Container Escape & Service Mesh Poisoning Range** | Status: Planned
*   [ ] **Project 27: Offensive Observability & Detection Engineering Inversion** | Status: Planned
*   [ ] **Project 28: Automated CI/CD Pipeline Attack & Supply Chain Range** | Status: Planned
*   [ ] **Project 29: Automated Active Directory Misconfiguration Graph Scanner** | Status: Planned

### Phase 10: Telemetry, Invariants, & Forensics
*   [ ] **Project 30: Kernel-Level System Tracer utilizing Linux eBPF Sandboxing** | Status: Planned
*   [ ] **Project 31: Low-Level Anomalous Flow Monitor via Windows ETW Streams** | Status: Planned
*   [ ] **Project 32: Behavioral Invariant Detection Engine (W\wedgeX Violation Tracker)** | Status: Planned
*   [ ] **Project 33: Direct Kernel Object Manipulation (DKOM) Volatile Memory Auditor** | Status: Planned

### Phase 11: Distributed Systems, Edge Protocols, & Internet-Scale Command Infrastructure
*   [ ] **Project 34: Decentralized, P2P Command & Control (C2) Mesh Over Nat** | Status: Planned
*   [ ] **Project 35: High-Performance, Zero-Copy Log Aggregator for Distributed Forensics** | Status: Planned
*   [ ] **Project 36: BGP Hijacking & Internet-Scale Route Leak Simulator** | Status: Planned
*   [ ] **Project 37: Web3/Blockchain-Based Bulletproof Stager Infrastructure** | Status: Planned
*   [ ] **Project 38: Distributed Byzantine Fault-Tolerant (BFT) Secret Sharing Network** | Status: Planned

### Phase 12: Planetary-Scale Operations, Autonomous Swarms, & Edge Cryptanalysis
*   [ ] **Project 39: Mass-Asymmetric Internet Scanner & Vulnerability Correlator** | Status: Planned
*   [ ] **Project 40: Autonomous C2 Swarm with Ephemeral Cloud-Edge Workers** | Status: Planned
*   [ ] **Project 41: Distributed Timing Attack & Side-Channel Network Analysis** | Status: Planned
*   [ ] **Project 42: Deep-Web / Darknet Metadata Harvester & Graph Link Analyzer** | Status: Planned
*   [ ] **Project 43: Autonomous Internet Censorship Circumvention Engine** | Status: Planned

### Phase 13: Orbital Mesh Infrastructures, Interplanetary Protocols, & Space-Edge Resiliency
*   [ ] **Project 44: Delay-Tolerant Networking (DTN) Bundle Protocol (RFC 9171) Router** | Status: Planned
*   [ ] **Project 45: Zero-Trust CubeSat Flight Software Runtime via WebAssembly (Wasm)** | Status: Planned
*   [ ] **Project 46: Ephemeris-Driven Kinetic Cryptographic Key Exchange** | Status: Planned

---

## Legal & Educational Disclaimer

The code, technical methodologies, architecture blueprints, and documentation provided across this entire portfolio (including all sub-directories, automation scripts, and associated experimental pipelines) are created strictly for educational, defensive security optimization, and authorized academic research purposes.

### 1. Authorized Testing & Containment Constraints
* **Isolated Testing Mandate:** Software, scripts, and packet-crafting utilities contained herein are designed to interact with low-level kernel stacks and network protocols. They are built to test edge-cases that may cause immediate system instability or unrecoverable kernel panics. Execution must be confined strictly to host-isolated, software-defined air-gapped laboratory environments (e.g., as outlined in SOP-SEC-LAB-01).
* **Explicit Authorization Required:** Under no circumstances should any utility or methodology within this repository be deployed against systems, networks, or infrastructure without explicit, prior written authorization from the verified infrastructure owner.

### 2. Limitation of Liability
* **No Warranty or Liability:** This software and information are provided "as-is" without warranty of any kind. The author assumes no liability, responsibility, or legal accountability for any misuse, unintended systemic disruption, data corruption, hardware damage, or illegal activity executed by third parties utilizing these materials. 
* **The "Domino Effect" Waiver:** Due to the complex architectural nature of cross-protocol research simulations (such as transport-to-routing layer interactions), the user assumes all risks regarding cascading failures or state-desynchronization anomalies within their testing environments.

### 3. Regulatory Compliance & Ethical Research
* **Legal Compliance:** Users are entirely responsible for ensuring their actions comply with all local, national, and international statutes regarding computer fraud, data privacy, and telecommunications security (e.g., the US Computer Fraud and Abuse Act, or regional equivalents).
* **Commitment to Responsible Disclosure:** The author is a dedicated advocate for global internet security and operates strictly under established Responsible Vulnerability Disclosure frameworks. Any zero-day vulnerabilities or systemic flaws discovered through the methodologies in this lab are reported directly to the affected vendors, maintainers, or appropriate coordination centers (e.g., CERT/CC, CISA) prior to any public architectural documentation.
