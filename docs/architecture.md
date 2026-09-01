# Proxmox VE Architecture

## Overview

This document summarizes the architecture of the **production Proxmox VE environment** documented in this case study.

Proxmox VE provides the virtualization layer for virtual machines and LXC containers, with dedicated compute, storage, and virtual networking resources.

## Architecture

```text
External Network Infrastructure
            │
            ▼
      Proxmox VE Host
            │
      ┌─────┴─────┐
      │           │
 Virtual Machines LXC Containers
      │           │
      └─────┬─────┘
            │
 Infrastructure & Business Workloads
```

The external network, firewalling, routing, and broader corporate infrastructure are intentionally outside the scope of this repository.

## What I Implemented

- Proxmox VE production virtualization environment
- Virtual machines and LXC containers
- CPU and memory allocation per workload
- Virtual disk and storage allocation
- Linux bridges and virtual network interfaces
- VLAN integration
- Administrative access controls
- Resource monitoring

## How I Administer It

My administration responsibilities include:

- Provisioning and removing virtual workloads
- Adjusting CPU, memory, storage, and network resources
- Managing VM and LXC lifecycle
- Monitoring host and workload resource utilization
- Managing virtual networking and storage
- Maintaining administrative access
- Troubleshooting hypervisor and workload-related issues
- Maintaining the Proxmox VE platform

## Scope

This documentation focuses only on the **Proxmox VE virtualization layer**.

Company-specific topology, external firewall configuration, remote-access infrastructure, DNS architecture, and other internal services are intentionally excluded.
