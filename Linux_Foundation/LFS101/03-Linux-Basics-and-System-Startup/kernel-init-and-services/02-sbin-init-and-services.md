# `/sbin/init` & The Process Hierarchy

## 1. What is `/sbin/init`?

Once the Linux kernel mounts the permanent root filesystem (`/`), its final task in the boot sequence is to execute the very first user-space program: **`/sbin/init`**.

```text
+-------------------------------------------------------------------------+
|                       LINUX PROCESS HIERARCHY TREE                      |
+-------------------------------------------------------------------------+
|                                                                         |
|                          [ Linux Kernel ]                               |
|                                 │                                       |
|               ┌─────────────────┴─────────────────┐                     |
|               ▼                                   ▼                     |
|       [ Kernel Space Threads ]            [ User Space (PID 1) ]        |
|         PID 2: [kthreadd]                   PID 1: /sbin/init           |
|         ├── [ksoftirqd/0]                 (systemd / SysVinit)          |
|         ├── [kworker/0:0]                         │                     |
|         └── [migration/0]         ┌───────────────┼───────────────┐     |
|                                   ▼               ▼               ▼     |
|                              [ sshd ]       [ NetworkMgr ]    [ agetty ]|
|                                   │                               │     |
|                              [ sshd session ]                [ /bin/login ]
|                                   │                               │     |
|                              [ bash ]                        [ bash ]   |
|                                   │                               │     |
|                              [ top ]                         [ vim ]    |
|                                                                         |
+-------------------------------------------------------------------------+
```

> [!NOTE]
> On modern systemd-based Linux distributions, `/sbin/init` is not a standalone executable; it is a **symbolic link** pointing to the systemd binary:
> ```bash
> $ ls -l /sbin/init
> lrwxrwxrwx 1 root root 20 /sbin/init -> /lib/systemd/systemd
> ```

---

## 2. Core Responsibilities of PID 1

As the root ancestor of all user space processes, `/sbin/init` (PID 1) performs four critical jobs:

### 1. Process Initiation & Service Management
- Starts essential background daemons (networking, firewall, logging, scheduled tasks, audio servers).
- Spawns login managers (graphical display manager or text console `getty` prompts).

### 2. The Universal Process Parent
- Every user process, script, shell, and desktop application is a direct or indirect descendant of PID 1.
- You can inspect this hierarchy live using the `pstree` or `ps -ef --forest` commands.

### 3. Process Reaping (Adopt Orphan Processes)
- If a parent process crashes or terminates before its children finish, those child processes become **orphans**.
- PID 1 automatically adopts orphaned processes. When they eventually exit, PID 1 reaps their exit status, preventing them from turning into permanent **zombie processes** that leak process IDs.

### 4. Clean System Shutdown & Reboot
- When powering off or rebooting, PID 1 coordinates the reverse sequence: terminating user sessions, stopping background daemons gracefully, syncing disk buffers to avoid data loss, and unmounting filesystems.

---

## 3. The Historical Standard: SysVinit

For decades, Linux relied on **SysVinit (System V Init)**, a mechanism derived from AT&T UNIX System V in the 1980s.

```text
SysVinit Boot Flow:
  /sbin/init reads /etc/inittab
        │
        ▼
  Determines Default Runlevel (e.g., Runlevel 3 or 5)
        │
        ▼
  Executes scripts in /etc/rc<N>.d/ sequentially:
    ├── S10network start   (Wait to finish...)
    ├── S20syslog start    (Wait to finish...)
    ├── S50sshd start      (Wait to finish...)
    └── S99local start     (Wait to finish...)
```

### The SysVinit Runlevel Model

| Runlevel | Mode / Purpose | Description |
| :--- | :--- | :--- |
| **0** | **Halt** | Shuts down the machine completely. |
| **1 / S** | **Single-User Mode** | Minimal maintenance mode; no networking, root login only. |
| **2** | **Multi-User (No Network)** | Multi-user text mode without NFS/network support. |
| **3** | **Multi-User (Full Network)** | Standard multi-user text-mode CLI (standard for servers). |
| **4** | **Unused / User-Defined** | Customizable by the system administrator. |
| **5** | **Graphical Mode** | Full multi-user environment with X11/GUI display manager. |
| **6** | **Reboot** | Gracefully terminates all processes and reboots the machine. |

---

## 4. SysVinit vs. Modern Init Systems

| Feature | Classic SysVinit | Modern `systemd` |
| :--- | :--- | :--- |
| **Execution Model** | **Sequential / Serial** (One script after another) | **Aggressive Parallelization** (Concurrent launches) |
| **Service Definitions** | Lengthy, fragile Bash shell scripts in `/etc/init.d/` | Clean, declarative `.service` unit files |
| **Process Tracking** | PID files (easy to lose track of child processes) | **Linux cgroups** (tracks every spawned sub-process) |
| **Configuration State** | Numbered symlinks in `/etc/rc0.d/` – `/etc/rc6.d/` | Target units (e.g., `multi-user.target`, `graphical.target`) |
| **Boot Speed** | Slow (bottlenecked by script execution times) | Extremely fast (launches non-dependent services in parallel) |