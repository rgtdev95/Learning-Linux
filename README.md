# Learning Linux 🐧

A structured repository for Linux notes, practical exercises, and cheat sheets based on **The Linux Foundation (LFS101: Introduction to Linux)** and hands-on system administration.

---

## 📚 Course Modules & Notes

### Linux Foundation: LFS101 - Introduction to Linux

> **Note:** The official LFS101 syllabus opens with a *Chapter 1: The Linux Foundation* (covering the organization itself, training format, and course requirements). It's intentionally skipped here since it's administrative rather than technical content — notes below start at the official Chapter 2 (Linux Philosophy and Concepts).

#### 1. [Chapter 02: Philosophy and Context](file:///c:/Users/ron/Documents/Ron-work/Learning-Linux/Linux_Foundation/LFS101/02-Philosphy-and-Context/overview.md)
- [Overview](file:///c:/Users/ron/Documents/Ron-work/Learning-Linux/Linux_Foundation/LFS101/02-Philosphy-and-Context/overview.md) — Chapter roadmap and learning objectives.
- [History and Evolution](file:///c:/Users/ron/Documents/Ron-work/Learning-Linux/Linux_Foundation/LFS101/02-Philosphy-and-Context/linux-history.md) — UNIX origins, GNU Project, Linus Torvalds, and modern milestones.
- [Linux Philosophy](file:///c:/Users/ron/Documents/Ron-work/Learning-Linux/Linux_Foundation/LFS101/02-Philosphy-and-Context/linux-philosphy.md) — Unix tenets, "everything is a file", pipes, daemons, and modularity.
- [Core Terminology & Architecture](file:///c:/Users/ron/Documents/Ron-work/Learning-Linux/Linux_Foundation/LFS101/02-Philosphy-and-Context/linux-terminology.md) — Kernel vs. user space, FHS, Shell, CLI/GUI, and open-source licensing.
- [Linux Distributions](file:///c:/Users/ron/Documents/Ron-work/Learning-Linux/Linux_Foundation/LFS101/02-Philosphy-and-Context/linux-distribution.md) — Distro anatomy, Debian/Red Hat/SUSE/Arch families, package management, and distro selection.
- [The Linux Community & Ecosystem](file:///c:/Users/ron/Documents/Ron-work/Learning-Linux/Linux_Foundation/LFS101/02-Philosphy-and-Context/linux-community.md) — Community channels, Linux Foundation, etiquette for asking questions, and ways to contribute.

#### 2. Chapter 03: Linux Basics and System Startup
##### Section A: [The Boot Process](file:///c:/Users/ron/Documents/Ron-work/Learning-Linux/Linux_Foundation/LFS101/03-Linux-Basics-and-System-Startup/the-boot-process/01-the-boot-process.md)
- [01. Boot Process Overview](file:///c:/Users/ron/Documents/Ron-work/Learning-Linux/Linux_Foundation/LFS101/03-Linux-Basics-and-System-Startup/the-boot-process/01-the-boot-process.md) — The 6 stages of Linux startup from power button to login.
- [02. BIOS & UEFI: First Steps](file:///c:/Users/ron/Documents/Ron-work/Learning-Linux/Linux_Foundation/LFS101/03-Linux-Basics-and-System-Startup/the-boot-process/02-bios-the-first-steps.md) — Power-on, POST diagnostics, CMOS/NVRAM, and boot device priority.
- [03. MBR, UEFI & Bootloaders](file:///c:/Users/ron/Documents/Ron-work/Learning-Linux/Linux_Foundation/LFS101/03-Linux-Basics-and-System-Startup/the-boot-process/03-mbr-efi-bootloader.md) — GRUB 2, ISOLINUX, U-Boot, and BIOS/MBR vs. UEFI/GPT comparison.
- [04. Boot Loader in Action](file:///c:/Users/ron/Documents/Ron-work/Learning-Linux/Linux_Foundation/LFS101/03-Linux-Basics-and-System-Startup/the-boot-process/04-boot-loader-in-action.md) — GRUB execution stages, interactive boot menu, kernel parameters, and decompression.
- [05. The Initial RAM Disk (initramfs)](file:///c:/Users/ron/Documents/Ron-work/Learning-Linux/Linux_Foundation/LFS101/03-Linux-Basics-and-System-Startup/the-boot-process/05-initial-ram-disk.md) — The storage chicken-and-egg dilemma, udev discovery, LUKS/LVM, and `switch_root`.
- [06. Virtual Terminals & Logins](file:///c:/Users/ron/Documents/Ron-work/Learning-Linux/Linux_Foundation/LFS101/03-Linux-Basics-and-System-Startup/the-boot-process/06-text-mode-login.md) — `systemd` PID 1, TTY console shortcuts, login authentication, and the shell REPL cycle.

##### Section B: [Kernel, Init & Services](file:///c:/Users/ron/Documents/Ron-work/Learning-Linux/Linux_Foundation/LFS101/03-Linux-Basics-and-System-Startup/kernel-init-and-services/01-the-linux-kernel.md)
- [01. The Linux Kernel](file:///c:/Users/ron/Documents/Ron-work/Learning-Linux/Linux_Foundation/LFS101/03-Linux-Basics-and-System-Startup/kernel-init-and-services/01-the-linux-kernel.md) — `start_kernel()`, memory mapping, multi-core setup, and early userspace handoff.
- [02. /sbin/init & Process Hierarchy](file:///c:/Users/ron/Documents/Ron-work/Learning-Linux/Linux_Foundation/LFS101/03-Linux-Basics-and-System-Startup/kernel-init-and-services/02-sbin-init-and-services.md) — PID 1 responsibilities, orphan process reaping, and classic SysVinit runlevels.
- [03. Linux Startup Alternatives](file:///c:/Users/ron/Documents/Ron-work/Learning-Linux/Linux_Foundation/LFS101/03-Linux-Basics-and-System-Startup/kernel-init-and-services/03-linux-startup-alternatives.md) — Why SysVinit evolved, Upstart event-driven model, and the rise of `systemd`.
- [04. Modern Service Management with systemd](file:///c:/Users/ron/Documents/Ron-work/Learning-Linux/Linux_Foundation/LFS101/03-Linux-Basics-and-System-Startup/kernel-init-and-services/04-systemd-features.md) — Unit anatomy, systemd targets, `systemctl` commands, and service status inspection.

##### Section C: [Understanding the Linux File System](file:///c:/Users/ron/Documents/Ron-work/Learning-Linux/Linux_Foundation/LFS101/03-Linux-Basics-and-System-Startup/understanding-linux-file-system/01-common-linux-filesystem-types.md)
- [01. Common Linux Filesystem Types](file:///c:/Users/ron/Documents/Ron-work/Learning-Linux/Linux_Foundation/LFS101/03-Linux-Basics-and-System-Startup/understanding-linux-file-system/01-common-linux-filesystem-types.md) — ext4, XFS, Btrfs, flash filesystems, and in-memory pseudo-filesystems (`/proc`, `/sys`, `tmpfs`).
- [02. Partitions, Filesystems & Mounting](file:///c:/Users/ron/Documents/Ron-work/Learning-Linux/Linux_Foundation/LFS101/03-Linux-Basics-and-System-Startup/understanding-linux-file-system/02-partitions-and-filesystem.md) — Storage analogy, device naming (`/dev/sda1`, `/dev/nvme0n1p1`), unified tree mounting, and Windows vs. Linux comparison.
- [03. The Filesystem Hierarchy Standard (FHS)](file:///c:/Users/ron/Documents/Ron-work/Learning-Linux/Linux_Foundation/LFS101/03-Linux-Basics-and-System-Startup/understanding-linux-file-system/03-the-filesystem-hierarchy-standard.md) — Complete FHS 3.0 directory reference, Windows/macOS mappings, and removable media automounting.
- [04. Case Sensitivity & The /usr Hierarchy](file:///c:/Users/ron/Documents/Ron-work/Learning-Linux/Linux_Foundation/LFS101/03-Linux-Basics-and-System-Startup/understanding-linux-file-system/04-closer-look-at-the-filesystem-hierarchy.md) — Case sensitivity rules, modern UsrMerge (`/bin -> /usr/bin`), and absolute vs. relative path navigation.
