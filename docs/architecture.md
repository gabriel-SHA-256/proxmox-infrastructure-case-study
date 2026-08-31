# Proxmox VE Lab Architecture

## Overview

This project documents a self-hosted virtualization environment built with Proxmox VE.

The environment is used for virtual machine administration, Linux server workloads, networking, storage management, GPU passthrough, service deployment, and infrastructure troubleshooting.

## Architecture

```text
Physical Server
│
└── Proxmox VE
    │
    ├── Virtual Networking
    │
    ├── Storage
    │
    └── Virtual Machines
        │
        └── Ubuntu Server
            ├── Linux services
            ├── SSH administration
            ├── systemd services
            └── NVIDIA GPU passthrough
```

## Proxmox VE Host

The physical host runs **Proxmox VE** as the virtualization platform.

Main administration tasks include:

- Virtual machine creation and management
- CPU and memory allocation
- Virtual networking
- Storage management
- VM disk management
- PCIe device passthrough
- VM console access
- Infrastructure troubleshooting

## Virtual Machines

Linux virtual machines are deployed and administered through Proxmox VE.

Tasks include:

- VM provisioning
- CPU and RAM configuration
- Virtual disk configuration
- Network interface configuration
- Linux installation
- SSH remote administration
- Service management
- Resource monitoring
- Troubleshooting

## GPU Passthrough

An Ubuntu Server virtual machine uses **PCIe passthrough** to access an NVIDIA GPU directly.

The configuration includes:

- PCIe device identification
- IOMMU configuration
- Proxmox PCI passthrough
- NVIDIA driver installation inside the VM
- CUDA configuration
- GPU validation

Example validation:

```bash
nvidia-smi
```

## Networking

Virtual machines use Proxmox virtual networking to communicate with the local network.

Administration and troubleshooting include:

- Linux bridges
- Virtual network interfaces
- TCP/IP configuration
- Routing validation
- SSH connectivity
- Network troubleshooting

Useful commands:

```bash
ip addr
ip route
ping <destination>
ss -tulpn
```

## Storage

Storage administration includes:

- Virtual disk allocation
- Storage capacity monitoring
- VM disk expansion
- Linux filesystem expansion
- Storage troubleshooting

Useful commands:

```bash
lsblk
df -h
```

## Troubleshooting

Common troubleshooting tasks in this environment include:

- Checking VM resource utilization
- Diagnosing Linux services
- Troubleshooting network connectivity
- Expanding virtual disks
- Validating PCIe GPU passthrough
- Reviewing system logs
- Managing systemd services

Useful commands:

```bash
systemctl status <service>
journalctl -u <service>
free -h
df -h
lsblk
ip addr
ip route
```

## Security

Sensitive information is intentionally excluded from this public repository.

The documentation does not contain:

- Passwords
- Authentication tokens
- SSH private keys
- Public IP addresses
- Internal credentials
- Sensitive host configuration
