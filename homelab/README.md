# Homelab Infrastructure & Environment Blueprints

This directory contains the infrastructure-as-code configurations, provisioning playbooks, and standard operating procedures required to instantiate a secure, software-defined air-gapped laboratory environment.

## Directory Layout

* **[`networks/`](./networks/)**: Contains KVM/QEMU virtual XML switch definitions for local containment.
* **[`provisioning/`](./provisioning/)**: Contains automated script components to deploy disposable target systems.
* **[`docs/`](./docs/)**: Houses deployment standards and technical documentation.

## Getting Started
To stand up the host-isolated environment, proceed directly to the operational guide:
**[SOP-SEC-LAB-01: Baseline Sandbox Deployment](./docs/SOP-SEC-LAB-01.md)**
