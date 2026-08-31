# Proxmox VE Security Hardening

## Overview

This document describes security measures and administrative access controls applied in my **Proxmox VE infrastructure lab**.

The focus is on protecting hypervisor administration, reducing unnecessary privileged access, separating infrastructure workloads, and using network controls to limit access between environments.

## Administrative Access

Administrative access to Proxmox VE has been configured with additional authentication controls.

The environment has included:

- Two-factor authentication (2FA) for Proxmox VE access
- Restricted use of the root account for routine administration
- Dedicated administrative access to the Proxmox VE management interface
- Local console access as a recovery path for administrative access issues

These controls reduce reliance on a single unrestricted administrative account.

## Privileged Access

The root account is not intended for normal day-to-day administration.

Privileged access is reserved for tasks that specifically require elevated permissions, while routine management is performed through controlled administrative access.

This reduces unnecessary use of unrestricted privileges on the hypervisor.

## Administrative Recovery

Administrative recovery has been performed directly through the **local Proxmox VE console** when remote authentication access was unavailable.

Using local console access provides a recovery path without depending on an externally exposed recovery mechanism.

## Network Segmentation

The Proxmox environment is integrated with a segmented network architecture using **pfSense and VLANs**.

Network segmentation is used to separate infrastructure traffic and control communication between network segments.

pfSense provides:

- Firewall policy enforcement
- Routing between network segments
- VLAN gateway control
- Access control between infrastructure networks

This allows virtualized workloads and infrastructure services to operate within defined network boundaries.

## Hypervisor and Workload Separation

Application and infrastructure workloads are deployed inside virtual machines instead of directly on the Proxmox VE host whenever appropriate.

This keeps the hypervisor focused on virtualization responsibilities and limits direct interaction between guest workloads and the underlying host.

The separation provides distinct administrative boundaries between:

**Proxmox VE Host → Virtual Machines → Workloads**

## Management Practices

Security-related administration of the Proxmox VE environment includes:

- Maintaining the hypervisor through supported repositories and system updates
- Reviewing administrative access after authentication changes
- Separating hypervisor administration from guest workload administration
- Limiting direct privileged access
- Maintaining a local administrative recovery path
- Using firewall and VLAN controls at the network layer

## Security Scope

Security in this lab is treated across multiple layers:

- **Identity and authentication** — administrative accounts and 2FA
- **Privilege management** — restricted root usage
- **Hypervisor isolation** — separation between Proxmox VE and guest workloads
- **Network security** — pfSense firewall policies and VLAN segmentation
- **Administrative recovery** — local console access
- **Platform maintenance** — hypervisor maintenance and update management

These controls are applied as part of the overall infrastructure architecture rather than as isolated security features.
