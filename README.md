# Proxmox VE Infrastructure Case Study

> This repository is a sanitized case study based on a **production Proxmox VE environment** that I implemented and currently administer. Company-specific identifiers, network addressing, credentials, hostnames, and sensitive configuration details have been removed or anonymized.

## Overview

The environment uses **Proxmox VE** as the virtualization platform for production virtual machines and LXC containers supporting business and infrastructure workloads.

My responsibilities cover workload provisioning, resource management, virtual networking, storage administration, access control, monitoring, and infrastructure troubleshooting.

## Tech Stack

- Proxmox VE
- Linux
- Virtual Machines
- LXC Containers
- Linux Bridges
- VLANs
- Virtual Networking
- Virtual Storage
- Two-Factor Authentication (2FA)

## Responsibilities & Implementation

I implemented and currently administer the Proxmox VE virtualization layer, including:

- Provisioning and lifecycle management of VMs and LXC containers
- CPU and memory allocation according to workload requirements
- Virtual disk provisioning, expansion, and capacity management
- Linux bridge and virtual network interface configuration
- VLAN integration for segmented workload connectivity
- Host and workload resource monitoring
- Administrative access management with 2FA
- Proxmox VE platform maintenance
- Infrastructure troubleshooting across hypervisor, storage, networking, and guest layers

## Technical Documentation

- [Architecture](docs/architecture.md)
- [VM Provisioning](docs/vm-provisioning.md)
- [Virtual Networking](docs/networking.md)
- [Storage Management](docs/storage.md)
- [Security Hardening](docs/security-hardening.md)

## Infrastructure Evidence

The screenshots below are sanitized views from the production Proxmox VE environment.

### Datacenter Overview

![Proxmox VE Datacenter](screenshots/proxmox-datacenter-overview.jpeg)

Production Proxmox VE environment showing active workloads and host resource utilization.

### Resources

![Proxmox VE Resources](screenshots/proxmox-resources-overview.jpeg)

Overview of virtual machines, LXC containers, and storage resources administered through Proxmox VE.

### Virtual Machine Hardware

![Virtual Machine Hardware](screenshots/proxmox-vm-hardware.jpeg)

Example of a production VM configuration with allocated CPU, memory, virtual storage, and network resources.

### Virtual Networking

![Proxmox VE Networking](screenshots/proxmox-networking.jpeg)

Production Proxmox VE networking configuration using Linux bridges and VLAN interfaces for virtual workloads.
