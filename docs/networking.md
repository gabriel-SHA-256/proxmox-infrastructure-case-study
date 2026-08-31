# Proxmox VE Networking

## Overview

This document describes the network architecture and configuration used in my **Proxmox VE infrastructure lab**.

The environment integrates Proxmox VE with **pfSense, VLAN segmentation, a managed switch, virtual networking, routing, firewall rules, and DNS services**.

## Network Architecture

```text
Internet
   │
   ▼
pfSense
   │
   ├── LAN
   │
   └── VLAN
         │
         ▼
   Managed Switch
         │
         ▼
   Proxmox VE Host
         │
         ├── Virtual Machines
         └── Infrastructure Services
```

## Proxmox Virtual Networking

Proxmox VE virtual networking is used to connect virtual machines to the physical network infrastructure.

The environment includes:

- Linux bridges
- Virtual network interfaces
- VLAN-aware networking
- Connectivity between virtual machines and external network services
- Integration between the Proxmox host and the managed network infrastructure

Virtual machines can be connected to different network segments depending on the requirements of each workload.

## VLAN Segmentation

The lab uses VLANs to separate infrastructure traffic into dedicated network segments.

The implementation involved:

- VLAN configuration on pfSense
- VLAN tagging through a managed switch
- VLAN configuration on the Proxmox VE host
- Virtual interfaces associated with the VLAN
- Routing and firewall control through pfSense

This environment was also used to troubleshoot VLAN connectivity between Proxmox VE and pfSense.

One troubleshooting case involved correcting the VLAN interface configuration on the Proxmox host and validating that tagged traffic was successfully reaching pfSense.

## pfSense Integration

pfSense operates as the firewall and routing platform for the lab network.

Its responsibilities include:

- Routing between network segments
- VLAN gateway configuration
- Firewall rule management
- Network access control
- DNS integration
- Connectivity between infrastructure services

The integration with Proxmox VE allows virtual workloads to use the same segmented network architecture as physical devices.

## Managed Switch

A managed switch is used to transport VLAN traffic between pfSense and the Proxmox VE host.

The switch configuration includes tagged VLAN traffic on the links involved in the virtualized infrastructure.

This provides end-to-end VLAN connectivity across:

**pfSense → Managed Switch → Proxmox VE → Virtual Workloads**

## DNS Services

The lab also includes **Pi-hole** integrated with the network infrastructure for DNS services.

DNS traffic is coordinated with pfSense, providing centralized DNS configuration for devices and virtual workloads in the environment.

## Network Validation

After network changes, connectivity is validated across the complete path rather than only at the virtual machine level.

Validation includes:

- VLAN membership
- Tagged traffic between devices
- Proxmox virtual interface configuration
- Gateway reachability
- Routing between required networks
- Firewall behavior
- DNS resolution
- Connectivity between virtual workloads and infrastructure services

## Troubleshooting

Hands-on troubleshooting in this environment has included:

- Incorrect VLAN interface configuration
- VLAN tagging problems
- Proxmox virtual networking issues
- Connectivity between Proxmox VE and pfSense
- Routing and gateway problems
- Firewall rule validation
- DNS connectivity and resolution

The troubleshooting process follows the network path layer by layer, from the virtual workload through Proxmox VE, the managed switch, and pfSense.
