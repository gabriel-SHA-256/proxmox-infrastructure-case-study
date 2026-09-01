# Proxmox VE Security Hardening

## Overview

This document summarizes the security controls applied to the **production Proxmox VE environment** documented in this case study.

The focus is on protecting administrative access, reducing unnecessary privileged access, maintaining recovery options, and separating the hypervisor from guest workloads.

## What I Implemented

Security controls in the Proxmox VE environment include:

- Two-factor authentication (2FA)
- Restricted routine use of the root account
- Controlled administrative access to the Proxmox VE interface
- Local console access for administrative recovery
- Separation between hypervisor and guest workloads
- Platform maintenance and access review

## Administrative Access

Proxmox VE administrative access is protected with **two-factor authentication**.

Routine administration is performed without relying on unrestricted root access when elevated privileges are not required.

This keeps normal management separate from full hypervisor-level privileges.

## Hypervisor Separation

Virtual machines and LXC containers host infrastructure and business workloads, while the Proxmox VE host remains focused on virtualization and infrastructure management.

This separates:

**Proxmox VE Host → VMs / LXC Containers → Workloads**

and reduces unnecessary workload execution directly on the hypervisor.

## Administrative Recovery

Local console access is maintained as a recovery path for authentication or administrative access issues.

This recovery method has been used to restore access when normal remote administration was unavailable.

## Platform Maintenance

Security-related administration also includes:

- Maintaining the Proxmox VE platform
- Reviewing access after authentication changes
- Preserving hypervisor and workload separation
- Maintaining administrative recovery access

## Scope

This document covers only security controls directly related to the **Proxmox VE virtualization layer**.

External firewall policies, VPN infrastructure, corporate network security, and broader network segmentation are outside the scope of this repository.
