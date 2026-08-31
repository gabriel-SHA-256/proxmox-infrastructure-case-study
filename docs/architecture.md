# Proxmox VE Lab Architecture

## Overview

This project documents a self-hosted virtualization environment built with **Proxmox VE**.

The lab is used for virtual machine administration, Linux server workloads, storage services, networking, infrastructure testing, and troubleshooting.

The environment was designed to provide hands-on experience with virtualization and the integration between hypervisor, virtual machines, storage, and network services.

## Architecture

```text
Network / Internet
        │
        │
     pfSense
        │
        │
   Local Network
        │
        │
┌─────────────────────┐
│   Proxmox VE Host   │
│                     │
│  Virtual Networking │
│        │            │
│        ├── VM       │
│        ├── VM       │
│        ├── TrueNAS  │
│        └── Linux    │
│            Servers  │
│                     │
│      Storage        │
└─────────────────────┘
```

## Proxmox VE Host

The physical server runs **Proxmox VE** as the main virtualization platform.

The host is responsible for:

- Virtual machine lifecycle management
- CPU and memory allocation
- Virtual disk management
- Virtual networking
- Storage allocation
- VM console access
- Resource monitoring

## Virtual Machines

Multiple virtual machines can be deployed according to the requirements of each workload.

Examples used in the lab include:

- Linux server virtual machines
- Infrastructure service workloads
- TrueNAS
- Test and lab environments

Each VM receives its own virtual hardware configuration, including CPU, memory, storage, and network interfaces.

## Virtual Networking

Proxmox VE virtual networking connects the virtual machines to the physical network infrastructure.

The environment has been used with:

- Linux bridges
- Virtual network interfaces
- TCP/IP networking
- VLAN-based network segmentation
- pfSense routing and firewall services

Detailed network configuration is documented separately in `networking.md`.

## Storage

Storage is allocated and managed through Proxmox VE according to the requirements of each virtual machine.

The environment includes experience with:

- Virtual disk allocation
- VM storage management
- Disk capacity adjustments
- Storage-oriented virtual machines such as TrueNAS

Storage and backup procedures are documented separately in `storage-backup.md`.

## Administration

The environment is administered through the Proxmox VE management interface and guest operating system administration tools.

Typical activities include:

- Creating and removing virtual machines
- Adjusting CPU and memory
- Managing virtual disks
- Configuring virtual network interfaces
- Accessing VM consoles
- Monitoring resource utilization
- Troubleshooting infrastructure issues

## Security & Administrative Access

Administrative access to the Proxmox VE environment follows basic separation and access-control practices.

The lab has included:

- Two-factor authentication (2FA) for Proxmox VE administrative access
- Restricted use of the root account for routine administration
- Local console access for administrative recovery
- Separation between the Proxmox VE hypervisor and workloads running inside virtual machines
- Authenticated SSH access for remote administration of Linux guests

Security-specific configuration and hardening are documented separately from the general architecture.

## Documentation

This repository separates the main infrastructure topics into dedicated documents:

- [`vm-provisioning.md`](vm-provisioning.md) — Virtual machine creation and provisioning
- `networking.md` — Virtual networking, VLANs, routing, and connectivity
- `storage-backup.md` — Storage management and backup workflows
