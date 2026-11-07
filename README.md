# linux-virtualization-lab
Linux virtualization lab featuring QEMU/KVM, libvirt, Windows systems, and real-world troubleshooting.

# Linux Virtualization Lab

## Project Overview

This project documents my experience building and configuring a Windows virtualization environment on a Dell Precision 5560 running Pop!_OS Linux.

The goal is to create an isolated lab environment for Windows administration, PowerShell automation, infrastructure troubleshooting, and cybersecurity testing.

Throughout this project, I will document the installation process, configuration decisions, technical challenges, troubleshooting procedures, and lessons learned.

## Lab Environment

| Component | Configuration |
|---|---|
| Host Hardware | Dell Precision 5560 |
| Host Operating System | Pop!_OS 24.04 LTS |
| Processor | Intel Core i9-11950H |
| Memory | 64 GB |
| Virtualization | QEMU/KVM |
| Management | libvirt and virt-manager |
| Planned Guest OS | Windows 11 |

## Project Status: Paused — Host System Failure

**Date:** November 7, 2026

During the development of this virtualization lab, the Dell Precision 5560 running Pop!_OS experienced a critical system failure.

### Observed Symptoms
- The operating system reaches the graphical login screen.
- The system crashes again during or after the login process.
- No visible error message is provided.
- The system is currently unusable for continued lab development.

### Impact
The failure interrupted development of the QEMU/KVM virtualization environment before the Windows VM installation and validation could be completed.

### Troubleshooting Status
Root cause has not been determined. No confirmed relationship between the virtualization configuration and the operating system failure has been established.

### Decision
Further troubleshooting of the Dell Precision 5560 has been deferred to prioritize continued infrastructure development and professional portfolio work.

Development is transitioning to a Dell Precision 7670 running Windows 11 Pro, using Microsoft Hyper-V for virtualization.

### Lessons Learned
- Infrastructure projects can be interrupted by unexpected host failures.
- Technical documentation allows projects to be reviewed and resumed after an interruption.
- Separating project documentation from the host environment reduces the risk of losing work.
- Prioritizing project continuity can be more appropriate than immediately repairing a failed development system.

**Final Status:** Paused pending future hardware or operating system troubleshooting.
