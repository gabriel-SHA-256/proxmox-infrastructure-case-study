# Proxmox VE Architecture

## Overview

This document describes the architecture of the **production Proxmox VE virtualization layer** presented in this case study.

The environment is intentionally represented in a sanitized form. Company-specific hostnames, addressing, VLAN IDs, workload names, and external network details are not included.

## High-Level Architecture

```text
                 External Network Infrastructure
                            │
                            ▼
                   Physical Network
                            │
                            ▼
                 ┌────────────────────┐
                 │   Proxmox VE Host  │
                 │                    │
                 │  Linux Bridge(s)   │
                 │        │           │
                 │  VLAN Interfaces   │
                 │        │           │
                 │   ┌────┴────┐      │
                 │   │         │      │
                 │  VMs       LXC     │
                 │          Containers│
                 │                    │
                 │   Virtual Storage  │
                 └────────────────────┘
```

The Proxmox VE host provides the virtualization, virtual networking, and storage layer for production workloads.

Routing, firewalling, remote access, DNS architecture, and the broader corporate network are handled outside the scope of this repository.

## Architecture Decisions

### Hypervisor and Workload Separation

Business and infrastructure workloads run inside **virtual machines and LXC containers** rather than directly on the Proxmox VE host.

This keeps the hypervisor focused on virtualization and separates host administration from workload administration.

### VM and LXC Workloads

Both virtualization models are used according to workload requirements:

- **Virtual Machines** for workloads requiring a complete guest operating system and isolated virtual hardware
- **LXC Containers** for infrastructure services that can operate efficiently using container-based virtualization

### Virtual Networking

Proxmox VE uses **Linux bridges and VLAN interfaces** to connect virtual workloads to the production network.

The virtualization layer provides workload connectivity while routing and firewall policy remain external to Proxmox VE.

This keeps the hypervisor networking role focused on:

```text
Physical Network
       ↓
Proxmox VE Virtual Networking
       ↓
VM / LXC Network Interface
       ↓
Workload
```

### Network Segmentation

Virtual workloads can be attached to different network segments according to their infrastructure requirements.

VLAN integration is handled at the Proxmox VE layer without exposing the complete production VLAN topology in this public documentation.

### Storage Layer

VMs and LXC containers receive storage according to individual workload requirements.

Storage is managed separately from compute and networking resources, allowing disk capacity to be adjusted throughout the workload lifecycle.

Detailed storage administration is documented in [`storage.md`](storage.md).

## Design Boundaries

The architecture follows a clear separation between infrastructure layers:

```text
External Network & Security
            │
            ▼
     Proxmox VE Host
            │
   ┌────────┼────────┐
   │        │        │
Compute   Network   Storage
   │        │        │
   └────────┼────────┘
            ▼
       VM / LXC
            │
            ▼
         Workload
```

This separation makes it possible to troubleshoot and administer each layer independently without treating the Proxmox VE host as a general-purpose application server.

## Scope

This document covers only the **Proxmox VE virtualization architecture**.

The following are intentionally excluded:

- Complete corporate network topology
- Firewall configuration
- DNS infrastructure
- Remote-access infrastructure
- Internal workload names
- Production IP addressing
- VLAN identifiers
- Company-specific infrastructure details
