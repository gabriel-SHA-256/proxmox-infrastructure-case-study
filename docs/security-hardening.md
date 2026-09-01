# Proxmox VE Security Hardening

## Overview

This document describes security controls applied to the **production Proxmox VE environment** documented in this case study.

The focus is on protecting hypervisor administration, controlling privileged access, maintaining a recovery path for administrative access, separating the virtualization host from guest workloads, and maintaining the platform securely.

## Administrative Access

Administrative access to Proxmox VE is protected through controlled authentication mechanisms.

Controls implemented in the environment include:

- Two-factor authentication (2FA) for Proxmox VE administrative access
- Restricted use of the root account for routine administration
- Controlled access to the Proxmox VE management interface
- Local console access as an administrative recovery path

These measures reduce unnecessary reliance on unrestricted privileged access to the hypervisor.

## Privileged Access

Routine administration is performed without relying on direct root access whenever elevated privileges are not required.

Privileged access is reserved for operations that specifically require it.

This approach keeps day-to-day administration separated from unrestricted hypervisor-level privileges.

## Two-Factor Authentication

Two-factor authentication is enabled for administrative access to Proxmox VE.

This adds an additional authentication layer beyond account credentials and protects access to the virtualization management interface.

Authentication controls are treated independently from guest operating system access.

## Administrative Recovery

The environment maintains **local console access** as a recovery path for administrative access issues.

This recovery method has been used when normal administrative authentication was unavailable, allowing access to be restored directly from the Proxmox VE host without depending on remote recovery mechanisms.

## Hypervisor and Workload Separation

Infrastructure and application workloads are hosted inside **virtual machines and LXC containers** rather than being deployed directly on the Proxmox VE host when appropriate.

This maintains a separation between:

```text
Proxmox VE Hypervisor
        │
        ├── Virtual Machines
        └── LXC Containers
                │
             Workloads
```

The hypervisor remains focused on virtualization and infrastructure management, while workload administration remains within the corresponding guest environment.

## Management Plane Separation

Proxmox VE administration is treated separately from guest workload administration.

This distinction reduces unnecessary interaction between:

- Hypervisor administration
- Virtual machine administration
- LXC container administration
- Workload-level administration

Administrative actions are performed at the appropriate infrastructure layer rather than using the hypervisor as a general-purpose workload host.

## Platform Maintenance

Security administration also includes maintaining the Proxmox VE platform and reviewing administrative access following infrastructure or authentication changes.

Operational practices include:

- Maintaining the Proxmox VE platform through supported repositories
- Applying platform updates as part of infrastructure maintenance
- Reviewing administrative access after authentication changes
- Maintaining separation between hypervisor and guest workloads
- Preserving a local administrative recovery path

## Security Scope

The security controls documented in this case study are limited to the **Proxmox VE virtualization layer**.

They cover:

- **Authentication** — administrative accounts and two-factor authentication
- **Privilege management** — restricted routine use of root access
- **Management plane protection** — controlled hypervisor administration
- **Workload isolation** — separation between the hypervisor, VMs, and LXC containers
- **Administrative recovery** — local console recovery path
- **Platform maintenance** — maintenance of the Proxmox VE host

Corporate firewall policy, external network security, VPN infrastructure, and broader network segmentation are intentionally outside the scope of this repository.
