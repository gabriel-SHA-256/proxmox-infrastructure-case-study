# Virtual Machine Provisioning

## Overview

This document describes the virtual machine provisioning workflow used in the **production Proxmox VE environment** documented in this case study.

Virtual machines are provisioned according to workload requirements, with compute, memory, storage, networking, and guest operating system configuration defined before the workload is placed into service.

## Provisioning Workflow

The provisioning process includes:

1. Define the workload requirements
2. Select the appropriate compute and memory allocation
3. Configure virtual storage
4. Configure the virtual network interface
5. Deploy the guest operating system
6. Apply workload-specific guest configuration
7. Validate resources, connectivity, and service readiness
8. Adjust resources when operational requirements change

## Resource Allocation

CPU and memory are allocated according to the expected workload rather than using a fixed VM template for every system.

Relevant considerations include:

- Expected CPU utilization
- Memory requirements
- Workload growth
- Resource availability on the Proxmox VE host
- Impact on other virtualized workloads

Resources can be adjusted later as operational requirements change.

## Virtual Storage

Virtual disks are provisioned according to workload capacity requirements.

Storage configuration includes:

- Storage target selection
- Virtual disk sizing
- Controller configuration
- Capacity planning
- Disk expansion when required

Storage allocation is reviewed independently for each workload to avoid unnecessary over-allocation while maintaining sufficient operational capacity.

## Virtual Networking

Each VM is connected to the appropriate Proxmox VE virtual networking configuration.

Network provisioning includes:

- Virtual network interface assignment
- Linux bridge association
- Workload-specific network segment selection
- VLAN integration when required

Routing, firewall policy, and broader network security remain outside the virtualization layer.

## Guest Operating System Deployment

After the virtual hardware is defined, the guest operating system is deployed and configured according to the workload requirements.

Guest preparation can include:

- System identity and hostname configuration
- Network configuration
- Administrative access
- Storage preparation
- Required infrastructure or application services

The guest operating system is treated as a separate administration layer from the Proxmox VE hypervisor.

## Validation

Before a VM is considered ready for use, the relevant infrastructure layers are validated.

Validation includes:

- Successful VM startup
- Correct CPU and memory allocation
- Virtual disk availability
- Network interface operation
- Connectivity to required network resources
- Guest operating system availability
- Required workload services operating as expected

## Lifecycle Management

Provisioning does not end when the VM is initially created.

Ongoing VM administration includes:

- CPU and memory adjustments
- Virtual disk expansion
- Virtual hardware changes
- Network interface changes
- Console-based recovery or troubleshooting
- Resource utilization review
- Workload decommissioning when no longer required

Changes are evaluated according to the requirements and operational impact of the individual workload.
