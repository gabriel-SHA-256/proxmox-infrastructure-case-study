# Proxmox VE Storage & Backup

## Overview

This document describes the storage administration, capacity management, and backup workflows used in my **Proxmox VE infrastructure lab**.

The environment includes virtual disk management, storage capacity adjustments, **Proxmox Backup Server (PBS)**, and a **TrueNAS virtual machine** used as a storage-oriented workload.

## Storage Management

Storage resources in Proxmox VE are allocated according to the requirements of each virtual machine.

Administration activities include:

- Virtual disk provisioning
- VM storage allocation
- Storage utilization monitoring
- Virtual disk expansion
- Capacity management
- Storage-related troubleshooting

Storage allocations can be adjusted as workload requirements change.

## Virtual Disk Management

Virtual disks are created and managed through Proxmox VE.

Administration includes:

- Defining disk capacity during VM provisioning
- Expanding virtual disks when additional capacity is required
- Reviewing available storage before making changes
- Managing storage according to individual workload requirements

Virtual disk expansion involves both the **hypervisor layer** and the **guest operating system layer**, since additional capacity assigned in Proxmox VE must also be made available inside the guest.

## Capacity Management

Storage capacity is reviewed to identify:

- Increasing VM disk utilization
- Workloads approaching allocated capacity
- Available capacity for virtual disk expansion
- Backup storage consumption
- Storage requirements for additional workloads

Capacity is managed according to workload requirements rather than applying identical storage allocations to every VM.

## Backup Infrastructure

The lab includes **Proxmox Backup Server (PBS)** as part of the backup environment.

PBS provides a dedicated backup platform for workloads running on Proxmox VE.

The architecture separates active virtual workloads from the backup infrastructure:

```text
Virtual Machines
       │
       ▼
 Proxmox VE
       │
       ▼
Proxmox Backup Server
```

This provides a separate backup layer for virtual machines managed by Proxmox VE.

## Backup Administration

Backup-related administration includes:

- VM-level backup configuration
- Backup storage management
- Monitoring backup capacity
- Managing protected virtual workloads
- Reviewing backup availability

The objective is to maintain usable backup copies independently from the active VM disks.

## TrueNAS Workload

The environment also includes **TrueNAS running as a virtual machine on Proxmox VE**.

TrueNAS is treated as a storage-oriented workload with its own resource, disk, and network requirements.

It represents a different architectural role from Proxmox Backup Server:

- **Proxmox VE storage** provides storage resources for virtual machines
- **TrueNAS** provides storage services as a virtualized workload
- **Proxmox Backup Server** provides backup infrastructure for Proxmox workloads

Keeping these roles separate makes the storage architecture easier to manage and troubleshoot.

## Operational Considerations

Storage changes are evaluated with attention to:

- Available Proxmox storage capacity
- Current VM disk utilization
- Required disk expansion
- Backup storage consumption
- Impact on existing workloads
- Capacity required for additional virtual machines

## Troubleshooting

Storage-related troubleshooting in the environment has included:

- VM disk capacity limitations
- Virtual disk expansion
- Guest filesystem capacity after hypervisor-level disk expansion
- Storage allocation issues
- Backup storage capacity

Troubleshooting is approached by identifying the affected layer:

**Proxmox VE storage → virtual disk → guest operating system → backup infrastructure → workload**
