# Installing QEMU/KVM on Pop!_OS

## Project Objective

Configure a Linux-based virtualization environment capable of hosting Windows virtual machines for systems administration, PowerShell automation, infrastructure testing, and cybersecurity labs.

## Host Environment

| Component | Configuration |
|---|---|
| Computer | Dell Precision 5560 |
| Operating System | Pop!_OS 24.04 LTS |
| Processor | Intel Core i9-11950H |
| CPU | 8 cores / 16 threads |
| RAM | 64 GB |
| Virtualization Platform | QEMU/KVM |
| Management Software | libvirt, virt-manager |

## Step 1: Install Virtualization Packages

The following commands are provided in the reference guide:

```bash
sudo apt update
sudo apt install qemu-kvm libvirt-daemon-system libvirt-clients virt-manager bridge-utils
```

These packages provide the components required to create and manage virtual machines.

- **QEMU/KVM:** Provides hardware-assisted virtualization.
- **libvirt:** Provides virtualization management services.
- **virt-manager:** Provides a graphical interface for managing virtual machines.
- **bridge-utils:** Provides utilities for configuring Linux network bridges.

## Step 2: Enable the libvirt Service

```bash
sudo systemctl enable --now libvirtd
```

The command enables the service at startup and requests that it start immediately.

To inspect its status:

```bash
systemctl status libvirtd
```

During my configuration, the service was installed and enabled but showed an inactive status after shutting down successfully.

This prompted further investigation.

## Step 3: Configure User Permissions

The setup guide recommends adding the current Linux user to the `libvirt` group:

```bash
sudo usermod -aG libvirt $USER
```

A new login session is required before the updated group membership becomes active.

During troubleshooting, I discovered that my account did not initially belong to the `libvirt` group.

The investigation and remediation are documented separately in `02-libvirt-troubleshooting.md`.

## Step 4: Launch Virtual Machine Manager

```bash
virt-manager
```

The intended virtualization connection is:

**QEMU/KVM — System**

The initial connection attempt produced a permission-related error, requiring additional troubleshooting before proceeding with Windows installation.

## References

Initial installation procedure adapted from:

[Blake Faust — Setting Up a Windows Virtual Machine on Pop!_OS](https://blake-faust.com/posts/windows-vm-on-pop-os/)

This document records my implementation and troubleshooting experience using that guide.
