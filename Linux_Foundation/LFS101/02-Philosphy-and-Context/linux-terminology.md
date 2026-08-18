# Essential Linux Terminology & Architecture

## 1. System Architecture Overview

To navigate Linux effectively, you need a clear mental model of how its architectural layers interact.

```text
+-----------------------------------------------------------------------+
| USER SPACE (Ring 3 - Unprivileged)                                    |
|                                                                       |
|  +-----------------------------------------------------------------+  |
|  | Applications (Web Browsers, Editors, Web Servers, Database)     |  |
|  +-----------------------------------------------------------------+  |
|  | Shell (Bash, Zsh) & CLI Utilities (ls, grep, top, curl)         |  |
|  +-----------------------------------------------------------------+  |
|  | Desktop Environment (GNOME, KDE Plasma) / Display Server       |  |
|  +-----------------------------------------------------------------+  |
|  | System Libraries (glibc, libssl, libpthread)                    |  |
|  +-----------------------------------------------------------------+  |
+-----------------------------------┬-----------------------------------+
                                    │
                                    ▼
+-----------------------------------------------------------------------+
| SYSTEM CALL INTERFACE (API: read, write, open, fork, exec, socket)    |
+-----------------------------------┬-----------------------------------+
                                    │
                                    ▼
+-----------------------------------------------------------------------+
| KERNEL SPACE (Ring 0 - Privileged)                                    |
|                                                                       |
|  +-----------------------------------------------------------------+  |
|  | Linux Kernel Core                                               |  |
|  | (Process Scheduler, Virtual Memory, VFS Filesystem, Networking)|  |
|  +-----------------------------------------------------------------+  |
|  | Device Drivers & Loadable Kernel Modules (.ko)                  |  |
|  +-----------------------------------------------------------------+  |
+-----------------------------------┬-----------------------------------+
                                    │
                                    ▼
+-----------------------------------------------------------------------+
| HARDWARE (CPU, RAM, Disks / NVMe, Network Adapters, GPU, Peripherals) |
+-----------------------------------------------------------------------+
```

---

## 2. Core Concepts & Definitions

### The Kernel
- **Definition**: The central core of the operating system.
- **Role**: Sits between hardware and applications. Manages CPU scheduling, memory allocation, filesystem operations, peripheral hardware, and network communications.
- **Type**: Linux is a **monolithic kernel** with dynamic **Loadable Kernel Modules (LKMs)** that can load/unload device drivers at runtime without rebooting.

### Kernel Space vs. User Space
- **Kernel Space (Ring 0)**: A privileged memory domain where the kernel executes with unrestricted access to CPU instructions and physical hardware.
- **User Space (Ring 3)**: An isolated, unprivileged memory domain where applications, daemons, and user programs run.
- **System Calls (syscalls)**: The controlled gateway for user applications to request privileged actions (like reading a file or opening a network port) from the kernel.

### Shell, Terminal & Console
Often used interchangeably, but distinct:
- **Terminal Emulator**: A graphical application (e.g., GNOME Terminal, Alacritty, Konsole) that provides a window for entering text commands.
- **Shell**: The command-line interpreter that reads your typed commands, parses them, and tells the OS to execute them (e.g., `bash`, `zsh`, `fish`, `dash`).
- **Virtual Console / TTY**: Text-based screen sessions built into Linux (accessible via `Ctrl + Alt + F1` through `F6`).

### CLI vs. GUI
- **CLI (Command Line Interface)**: Interacting with the system via typed text commands. Highly automatable, remote-friendly (via SSH), and resource-efficient.
- **GUI (Graphical User Interface)**: Windows, icons, and menus powered by a **Display Server** (Wayland or X11) and a **Desktop Environment** (e.g., GNOME, KDE Plasma, XFCE).

### Daemons & Services
- **Daemon**: A non-interactive background process providing system services (e.g., `sshd` for remote access, `cron` for task scheduling).
- **Service Manager**: Software that manages the lifecycle of daemons (start, stop, restart, boot enable). **`systemd`** is the standard init and service manager on modern Linux.

---

## 3. Filesystem Hierarchy Standard (FHS)

Linux organizes all files and directories inside a single inverted tree originating at the **root directory (`/`)**.

| Directory | Purpose |
| :--- | :--- |
| **`/`** | **Root directory**. The top of the hierarchy; every file and folder starts here. |
| **`/bin`** & **`/usr/bin`** | Essential user command binaries (e.g., `ls`, `cp`, `bash`, `python`). |
| **`/sbin`** & **`/usr/sbin`** | System binaries intended for administrative tasks (e.g., `iptables`, `fdisk`, `reboot`). |
| **`/etc`** | Host-specific system-wide configuration files (e.g., `/etc/passwd`, `/etc/fstab`, `/etc/hosts`). |
| **`/home`** | Personal directories for regular users (e.g., `/home/ron/`). |
| **`/root`** | Home directory for the `root` administrative superuser. |
| **`/dev`** | Device files representing physical and virtual hardware (`/dev/sda`, `/dev/null`, `/dev/zero`). |
| **`/proc`** | Virtual pseudo-filesystem exposing real-time kernel & process state. |
| **`/sys`** | Virtual pseudo-filesystem exposing kernel objects, hardware devices, and drivers. |
| **`/var`** | Variable data that changes during system operation (logs in `/var/log`, databases, mail). |
| **`/tmp`** | Temporary files (often cleared automatically on reboot). |
| **`/opt`** | Optional add-on third-party software packages. |
| **`/mnt`** & **`/media`** | Mount points for temporary filesystems and removable media (USB drives, CD-ROMs). |

---

## 4. Users, Permissions & Privileges

Linux is built around strict access controls:
- **`root` (Superuser / UID 0)**: The all-powerful administrative account with unrestricted read/write/execute rights.
- **`sudo` (SuperUser DO)**: A command allowing authorized regular users to execute commands with elevated root privileges safely.
- **Standard Permissions**: Every file and directory has permissions assigned to three scopes:
  - **`u` (User / Owner)**: The specific user who owns the file.
  - **`g` (Group)**: The group assigned to the file.
  - **`o` (Others / World)**: Everyone else with an account on the system.
- **Permission Types**:
  - **`r` (Read - 4)**: View file content / list directory contents.
  - **`w` (Write - 2)**: Modify file content / create or delete files in directory.
  - **`x` (Execute - 1)**: Run file as a program / enter (`cd` into) a directory.

---

## 5. Software Packaging & Distribution

- **Package**: An archive file containing compiled application binaries, configuration files, metadata, and dependency lists.
- **Package Manager**: A tool that automates installing, upgrading, configuring, and removing packages while resolving dependencies automatically.
- **Repositories (Repos)**: Official, verified online servers where software packages are hosted and retrieved by the package manager.

---

## 6. Open Source Licensing & Standards

### POSIX (Portable Operating System Interface)
A set of IEEE standards defining API compatibility across UNIX and UNIX-like systems. Linux largely adheres to POSIX standards, allowing source code written for UNIX or macOS to compile and run on Linux.

### Licensing Types

```text
Open Source Licensing
├── Copyleft (Strict Share-Alike: Derivatives must stay open source)
│   ├── GNU GPLv2 (Used by the Linux Kernel)
│   ├── GNU GPLv3
│   └── GNU AGPL (Network / Cloud Copyleft)
│
└── Permissive (Flexible: Allows proprietary derivatives with attribution)
    ├── MIT License
    ├── Apache 2.0 (Includes explicit patent grant)
    └── BSD (2-Clause / 3-Clause)
```

- **Copyleft (e.g., GNU GPLv2 / GPLv3)**: Requires any derivative works or distributed modifications to also be open-sourced under the same license. The Linux kernel uses GPLv2.
- **Permissive (e.g., MIT, Apache 2.0, BSD)**: Allows anyone to freely use, modify, and redistribute code, even in proprietary commercial software, with minimal restrictions.
