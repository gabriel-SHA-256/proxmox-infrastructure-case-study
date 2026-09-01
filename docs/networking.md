# Proxmox VE Virtual Networking

## Overview

This document describes the **virtual networking layer of a production Proxmox VE environment** that I implemented and currently administer.

The Proxmox VE host provides network connectivity for virtual machines and LXC containers through Linux bridges, virtual network interfaces, and VLAN integration.

The broader corporate network, routing, firewalling, and external network security infrastructure are intentionally outside the scope of this repository.

## Network Architecture

```text
        External Network Infrastructure
                    │
                    │
          Physical Network Interface
                    │
                    ▼
         ┌─────────────────────┐
         │   Proxmox VE Host   │
         │                     │
         │   Linux Bridges     │
         │         │           │
         │   VLAN Interfaces   │
         │         │           │
         │   ┌─────┴─────┐     │
         │   │           │     │
         │  VMs      LXC Containers
         │                     │
         └─────────────────────┘
```

This diagram intentionally represents only the Proxmox VE networking layer and its connection to the external network infrastructure.

## Linux Bridges

Linux bridges are used to connect virtual workloads to the physical network.

They provide the network layer between:

**Physical interface → Proxmox VE → Virtual Machine / LXC Container**

Bridge configuration is managed according to the connectivity requirements of the workloads hosted on the Proxmox VE server.

## Virtual Network Interfaces

Virtual machines and LXC containers receive virtual network interfaces connected to the appropriate Proxmox VE networking configuration.

Administration includes:

- Virtual network interface assignment
- Bridge association
- Workload-specific network connectivity
- Interface changes during VM or container lifecycle management
- Troubleshooting connectivity between virtual workloads and the external network

## VLAN Integration

The production environment uses VLAN segmentation, with VLAN connectivity integrated into the Proxmox VE networking layer.

Proxmox-side configuration includes:

- VLAN interfaces
- VLAN-aware virtual networking
- Association between VLAN connectivity and virtual workloads
- Integration between the hypervisor networking layer and the external segmented network

VLAN routing and network security policy are handled outside Proxmox VE.

## Network Segmentation

Virtual workloads can be connected to different network segments according to their infrastructure requirements.

This allows the virtualization layer to support segmented connectivity without requiring all virtual machines and containers to share the same network context.

The Proxmox VE host is responsible for providing the appropriate virtual network path, while external infrastructure controls routing and communication between network segments.

## Production Troubleshooting

Networking work in this environment has included troubleshooting issues across the Proxmox VE virtual networking layer.

One production troubleshooting case involved an incorrect **VLAN interface configuration on the Proxmox VE host**.

The issue was isolated to the Proxmox networking layer, the VLAN interface configuration was corrected, and tagged traffic between the host and the external network infrastructure was successfully restored.

Other Proxmox-side networking troubleshooting includes:

- Virtual interface configuration
- Linux bridge configuration
- VLAN connectivity
- Workload network attachment
- Connectivity between virtual workloads and external infrastructure

## Administrative Scope

Networking administration documented in this repository is limited to the **Proxmox VE virtualization layer**.

The following are intentionally outside the scope of this case study:

- Corporate firewall configuration
- External routing configuration
- Complete VLAN topology
- DNS architecture
- Physical network topology
- Remote-access infrastructure
- Firewall policies and rules

This separation keeps the case study focused on the networking responsibilities directly associated with Proxmox VE.
