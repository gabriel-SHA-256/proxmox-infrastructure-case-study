# Proxmox VE Storage Management

## Overview

This document describes storage administration within the **production Proxmox VE environment** documented in this case study.

Storage resources are managed according to the requirements of virtual machines and LXC containers, with attention to capacity allocation, workload growth, virtual disk lifecycle, and operational impact.

This document focuses specifically on the **Proxmox VE storage layer**. External storage services and backup infrastructure are outside the scope of this repository.

## Storage Architecture

Proxmox VE manages multiple storage resources used by virtualized workloads.

At a high level:

```text
Proxmox VE Host
      │
      ├── Storage Resources
      │      │
      │      ├── VM Disks
      │      ├── LXC Volumes
      │      └── Installation Media
      │
      └── Virtual Workloads
             ├── Virtual Machines
             └── LXC Containers
```

Storage resources are assigned according to workload requirements rather than using a fixed allocation model across all virtual systems.

## Virtual Disk Management

Virtual disks are provisioned and managed through Proxmox VE throughout the VM lifecycle.

Administration includes:

- Virtual disk provisioning
- Storage target selection
- Capacity allocation
- Virtual disk expansion
- Disk reassignment when required
- Storage utilization monitoring
- Storage-related troubleshooting

Disk capacity can be adjusted when operational requirements change without rebuilding the virtual machine.

## LXC Storage

LXC containers also receive dedicated storage according to the requirements of the services they host.

Container storage administration includes:

- Volume allocation
- Capacity management
- Storage resource selection
- Expansion when required
- Monitoring storage consumption

VM and LXC storage are managed according to their individual workload characteristics.

## Capacity Management

Storage capacity is reviewed as part of ongoing infrastructure administration.

Relevant considerations include:

- Current storage utilization
- Growth of existing virtual workloads
- Available capacity for disk expansion
- Requirements for new VMs or containers
- Impact of allocation changes on the remaining storage pool

The objective is to maintain sufficient capacity for current workloads while preserving room for infrastructure growth.

## Disk Expansion

Virtual disk expansion is handled across separate infrastructure layers.

At the Proxmox VE level, additional capacity is assigned to the virtual disk.

The guest operating system is then responsible for consuming the additional capacity according to its own disk, partition, volume, and filesystem configuration.

This separation between **hypervisor storage** and **guest storage management** is considered when planning and troubleshooting disk expansion.

## Storage Allocation

Different workloads receive different storage allocations depending on their function and expected growth.

Storage decisions consider:

- Workload purpose
- Current capacity requirements
- Expected data growth
- Performance requirements
- Available Proxmox VE storage resources
- Impact on other virtualized workloads

This avoids unnecessary over-allocation while allowing resources to be expanded when justified by operational demand.

## Operational Administration

Storage-related administration in the environment includes:

- Reviewing storage consumption
- Provisioning disks for new workloads
- Expanding existing virtual disks
- Managing storage assigned to VMs and containers
- Evaluating available capacity before infrastructure changes
- Troubleshooting storage constraints
- Coordinating hypervisor-level storage changes with guest operating systems

## Troubleshooting

Storage troubleshooting is approached by identifying the affected layer before making changes.

Relevant layers include:

**Proxmox VE storage → virtual disk or container volume → guest operating system → workload**

Issues handled at the Proxmox VE storage layer include:

- Insufficient allocated capacity
- Virtual disk expansion requirements
- Storage resource availability
- Workload storage allocation
- Capacity constraints affecting virtualized systems
