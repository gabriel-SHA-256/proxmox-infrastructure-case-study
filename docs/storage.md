# Proxmox VE Storage Management

## Overview

This document summarizes how I manage storage in the **production Proxmox VE environment** documented in this case study.

Storage is allocated according to workload requirements for virtual machines and LXC containers, with attention to capacity, expansion, and operational impact.

## What I Manage

Within Proxmox VE, I manage:

- Virtual disk provisioning
- Storage allocation for VMs and LXC containers
- Disk capacity adjustments
- Storage target selection
- Storage utilization
- Workload-specific storage requirements

## Storage Allocation

Storage is assigned according to the needs of each workload rather than using the same allocation model for every VM or container.

My storage decisions consider:

- Current capacity requirements
- Expected workload growth
- Available Proxmox VE storage
- Impact on other virtualized workloads

## Disk Expansion

When additional capacity is required, I expand virtual disks through Proxmox VE and coordinate the change with the guest operating system.

This requires handling storage at separate layers:

**Proxmox VE storage → virtual disk or container volume → guest operating system**

## Capacity Management

Ongoing storage administration includes:

- Reviewing storage consumption
- Monitoring available capacity
- Planning disk expansion
- Allocating storage for new workloads
- Adjusting existing virtual disks
- Preventing capacity constraints from affecting running workloads

## Administration

My storage-related responsibilities include:

- Provisioning disks for new workloads
- Expanding existing virtual disks
- Managing storage assigned to VMs and containers
- Reviewing capacity before infrastructure changes
- Troubleshooting storage allocation and capacity issues

## Troubleshooting

Storage troubleshooting is performed by identifying the affected layer before making changes.

Typical issues include:

- Insufficient virtual disk capacity
- Storage allocation problems
- Capacity constraints
- Guest storage not reflecting hypervisor-level changes
