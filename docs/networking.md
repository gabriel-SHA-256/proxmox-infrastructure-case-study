# Proxmox VE Virtual Networking

## Overview

This document summarizes how I configure and manage virtual networking in the **production Proxmox VE environment** documented in this case study.

The Proxmox VE host provides the virtualization-side network layer for virtual machines and LXC containers, while routing, firewalling, and broader network security are handled outside the hypervisor.

## What I Configure

Within Proxmox VE, I manage:

- Linux bridges
- Virtual network interfaces
- VLAN interfaces
- VLAN-aware networking
- Network attachment for VMs and LXC containers
- Workload connectivity to segmented networks

## Network Integration

Virtual workloads are connected to the appropriate network segment according to their infrastructure requirements.

The Proxmox VE networking layer integrates virtual machines and containers with the external network infrastructure without placing routing or firewall responsibilities on the hypervisor.

## VLAN Integration

VLAN connectivity is used when workloads require network segmentation.

My Proxmox-side responsibilities include:

- VLAN interface configuration
- Bridge integration
- Virtual interface assignment
- Workload network attachment
- Validation of segmented connectivity

## Administration

Ongoing networking administration includes:

- Managing Linux bridges
- Adjusting VM and LXC network interfaces
- Maintaining VLAN integration
- Reviewing workload network attachment
- Troubleshooting Proxmox-side connectivity issues
- Coordinating networking changes with workload requirements

## Troubleshooting

When connectivity issues occur, I isolate the affected layer before making changes.

Proxmox-side troubleshooting includes:

- Virtual interface configuration
- Linux bridge configuration
- VLAN attachment
- Workload network assignment
- Connectivity between virtual workloads and the external network infrastructure

## Scope

This document covers only the **Proxmox VE virtual networking layer**.

External firewall policies, routing configuration, physical network topology, DNS infrastructure, and remote-access systems are outside the scope of this repository.
