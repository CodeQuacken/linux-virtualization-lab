# Troubleshooting: Libvirt Connection Failure

## Environment

- **Host:** Dell Precision 5560
- **Operating System:** Pop!_OS 24.04 LTS
- **Virtualization:** QEMU/KVM, libvirt, virt-manager

## Problem Description

While configuring a Windows virtual machine through Virtual Machine Manager, I encountered the following error:

`Unable to connect to libvirt qemu:///system. Verify that the libvirtd daemon is running.`

The error prevented Virtual Machine Manager from connecting to the system virtualization service.

## Investigation

### 1. Verify the libvirt service

I checked the service status:

```bash
systemctl status libvirtd
```

The output indicated:

- Service installed and enabled
- Status: `inactive (dead)`
- Last exit: `status=0/SUCCESS`
- Socket activation configured

**Finding:** The daemon had exited successfully rather than reporting a failure. This suggested that an inactive service alone might not explain the connection problem.

### 2. Test connectivity with elevated privileges

```bash
sudo virsh -c qemu:///system list --all
```

**Result:** Successful connection. No virtual machines were listed.

**Finding:** Libvirt was accessible with administrator privileges.

### 3. Test connectivity as the regular user

```bash
virsh -c qemu:///system list --all
```

**Result:** Permission denied.

**Finding:** The connection issue appeared related to user permissions rather than a failed virtualization service.

### 4. Examine user group membership

```bash
groups
```

**Result:**

```text
quacken adm sudo lpadmin
```

The account was not a member of the `libvirt` group.

## Remediation

The following command was selected to grant the user access to libvirt:

```bash
sudo usermod -aG libvirt quacken
```

A new login session is required for updated group membership to take effect.

## Verification Status

**Pending verification.**

The next step is to confirm that the regular user can connect using:

```bash
virsh -c qemu:///system list --all
```

Successful verification will confirm that the permissions change resolved the connection issue.

## Lessons Learned

- An inactive systemd service does not necessarily indicate a failed service.
- Socket activation can start services when requested.
- Testing commands with and without elevated privileges helps isolate permission issues.
- Linux group membership can affect access to virtualization services.
- Troubleshooting documentation should distinguish suspected causes from verified solutions.
