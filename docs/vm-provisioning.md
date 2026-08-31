# Virtual Machine Provisioning

## Overview

This document describes the standard process I use to create and provision a virtual machine in **Proxmox VE**.

The objective is to configure the required virtual hardware, install the guest operating system, and validate that the VM is ready for use.

## 1. Create the Virtual Machine

In the Proxmox VE web interface:

1. Select the Proxmox node.
2. Click **Create VM**.
3. Define the VM ID and hostname.
4. Select the operating system installation ISO.

## 2. Configure Virtual Hardware

Configure the VM according to the workload requirements.

### CPU

Define:

- Number of CPU sockets
- Number of CPU cores
- CPU type when required

### Memory

Allocate RAM based on the expected workload.

Memory can be increased or reduced later if requirements change.

### Storage

Create the virtual disk and define:

- Storage location
- Disk size
- Disk controller
- Disk format and options when required

### Network

Attach a virtual network interface to the appropriate Proxmox bridge.

Typical configuration includes:

- Bridge selection
- VirtIO network adapter
- Firewall option when required

## 3. Review the Configuration

Before creating the VM, review:

- VM ID
- Operating system
- CPU allocation
- Memory allocation
- Virtual disk
- Network interface

After validation, create the virtual machine.

## 4. Install the Guest Operating System

Start the VM and open the Proxmox console.

Boot from the attached ISO and complete the operating system installation.

After installation:

1. Remove or detach the installation media if necessary.
2. Configure the boot order.
3. Restart the VM.
4. Confirm that the guest operating system boots correctly.

## 5. Configure the Guest

After the operating system is running, complete the required guest configuration.

Depending on the workload, this can include:

- Hostname configuration
- Network configuration
- Administrative user configuration
- Remote access
- Storage preparation
- Required services and packages

## 6. Validate the VM

Before placing the VM into use, verify:

- VM boots successfully
- CPU resources are available
- Allocated memory is available
- Virtual disk is detected
- Network interface is operational
- Network connectivity is working
- Required services are running

## 7. Resource Adjustment

CPU, memory, storage, and other virtual hardware can be adjusted later when workload requirements change.

Typical VM administration tasks include:

- Increasing CPU or memory
- Expanding virtual disks
- Adding or removing virtual devices
- Modifying network interfaces
- Changing boot configuration
- Using the Proxmox console for troubleshooting
