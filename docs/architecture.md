# Proxmox VE Production Architecture

## Overview

This document presents a **sanitized representation of a production Proxmox VE environment** that I implemented and currently administer.

Proxmox VE provides the virtualization layer for business and infrastructure workloads running as virtual machines and LXC containers.

The architecture separates compute, virtual networking, storage, workload administration, and external network integration while keeping sensitive production details outside the public documentation.

## Architecture

```text
                 External Network Infrastructure
                            │
                            │
                  ┌─────────▼─────────┐
                  │   Proxmox VE Host │
                  │                   │
                  │  Virtual Network  │
                  │  ├─ Linux Bridges│
                  │  └─ VLAN Interfaces
                  │         │         │
                  │   ┌─────┴─────┐   │
                  │   │           │   │
                  │  VMs         LXC  │
                  │   │        Containers
                  │   │           │   │
                  │   └─────┬─────┘   │
                  │         │         │
                  │ Infrastructure &  │
                  │ Business Workloads│
                  │                   │
                  │      Storage      │
                  └───────────────────┘
```

The diagram intentionally represents only the Proxmox VE layer and its direct integration points. The complete corporate network topology is outside the scope of this repository.

## Proxmox VE Host

The physical server runs **Proxmox VE** as the production virtualization platform.

The host provides:

- Virtual machine lifecycle management
- LXC container lifecycle management
- CPU and memory resource allocation
- Virtual disk management
- Virtual networking
- Storage allocation
- Console access
- Resource monitoring
- Administrative control of virtualized workloads

## Virtual Machines

Virtual machines are provisioned according to the technical requirements of each workload.

VM administration includes:

- Virtual hardware configuration
- CPU and memory allocation
- Virtual disk management
- Network interface configuration
- Guest operating system deployment
- Resource adjustment
- Lifecycle management
- Infrastructure troubleshooting

The VM provisioning workflow is documented separately in [`vm-provisioning.md`](vm-provisioning.md).

## LXC Containers

Proxmox VE also hosts **LXC containers used for infrastructure services**.

Containers are managed independently from virtual machines and receive workload-specific compute, storage, and network resources.

Container administration includes:

- Resource allocation
- Storage assignment
- Virtual network configuration
- Service availability
- Lifecycle management
- Resource monitoring

Specific internal services are intentionally not enumerated in the public architecture documentation.

## Virtual Networking

Proxmox VE provides the virtualization-side network layer for VMs and LXC containers.

The environment includes:

- Linux bridges
- Virtual network interfaces
- VLAN interfaces
- Segmented network connectivity
- Integration with external network infrastructure

Routing, firewall policy, and broader network security functions are handled outside the Proxmox VE platform.

This separation maintains a clear boundary between the **virtualization layer** and the **external network/security layer**.

Detailed Proxmox networking documentation is available in [`networking.md`](networking.md).

## Storage

Storage resources are managed through Proxmox VE and allocated according to workload requirements.

Storage administration includes:

- VM and container disk allocation
- Capacity management
- Virtual disk expansion
- Storage utilization monitoring
- Workload-specific storage allocation
- Storage-related troubleshooting

Storage architecture is documented separately in [`storage.md`](storage.md).

## Administration

Operational administration of the environment includes:

- Provisioning and maintaining VMs and LXC containers
- Adjusting compute, memory, and storage resources
- Managing virtual networking
- Monitoring host and workload resource utilization
- Managing virtual disks and network interfaces
- Accessing workload consoles when required
- Troubleshooting issues across the hypervisor and guest layers
- Maintaining the Proxmox VE platform in production

## Administrative Security

Administrative access to the Proxmox VE platform is separated from normal guest workload administration.

Controls implemented in the environment include:

- Two-factor authentication for Proxmox VE administrative access
- Restricted use of privileged accounts for routine administration
- Local console access as an administrative recovery path
- Separation between the hypervisor and guest workloads

Security controls are documented separately in [`security-hardening.md`](security-hardening.md).

## Scope

This case study intentionally documents the **Proxmox VE virtualization layer only**.

External firewall platforms, corporate network architecture, internal service topology, remote-access implementation, and company-specific infrastructure details are outside the scope of this repository.
