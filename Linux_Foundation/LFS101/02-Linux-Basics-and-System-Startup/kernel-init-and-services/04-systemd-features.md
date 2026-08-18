# Modern Service Management with `systemd` & `systemctl`

## 1. Core Architecture & Advantages of `systemd`

**`systemd`** is a suite of basic building blocks for a Linux system. It provides a system and service manager that runs as **PID 1** and coordinates the rest of the operating system.

```text
+-------------------------------------------------------------------------+
|                        KEY ARCHITECTURAL PILLARS                        |
+-------------------------------------------------------------------------+
|                                                                         |
|  1. Aggressive Parallelization & Socket Activation                      |
|     └─ systemd creates listening sockets for all daemons before         |
|        starting them. This allows dependent services to launch          |
|        simultaneously without blocking or failing on startup.           |
|                                                                         |
|  2. Declarative Unit Files                                              |
|     └─ Replaces complex 100-line shell scripts with clean, readable     |
|        configuration files (.service, .target, .socket, .timer).        |
|                                                                         |
|  3. Linux Control Groups (cgroups) Integration                          |
|     └─ Every process launched by a service is tracked in a cgroup.      |
|        Stopping a service guarantees that all child and grandchild      |
|        worker processes are cleanly terminated without orphan leaks.    |
|                                                                         |
|  4. Dynamic On-Demand Activation                                        |
|     └─ Services can be started only when accessed via network socket,   |
|        D-Bus message, file path modification, or timed calendar event.  |
|                                                                         |
+-------------------------------------------------------------------------+
```

---

## 2. Anatomy of a systemd `.service` Unit File

Instead of imperative shell code, a systemd service is defined declaratively (e.g., `/lib/systemd/system/nginx.service`):

```ini
[Unit]
Description=A high performance web server and a reverse proxy server
Documentation=man:nginx(8)
After=network.target remote-fs.target nss-lookup.target

[Service]
Type=forking
PIDFile=/run/nginx.pid
ExecStartPre=/usr/sbin/nginx -t -q -g 'daemon on; master_process on;'
ExecStart=/usr/sbin/nginx -g 'daemon on; master_process on;'
ExecReload=/usr/sbin/nginx -g 'daemon on; master_process on;' -s reload
ExecStop=-/sbin/start-stop-daemon --quiet --stop --retry QUIT/5 --pidfile /run/nginx.pid
TimeoutStopSec=5
KillMode=mixed

[Install]
WantedBy=multi-user.target
```

- **`[Unit]`**: Metadata, human-readable descriptions, and dependency ordering (`After=`, `Requires=`, `Wants=`).
- **`[Service]`**: Execution commands (`ExecStart=`, `ExecStop=`, `ExecReload=`), service type, restart policies, and resource limits.
- **`[Install]`**: Specifies which target unit should pull this service in when enabled (`WantedBy=`).

---

## 3. Runlevels vs. `systemd` Targets

`systemd` replaces old numeric SysVinit runlevels with descriptive **target units** (`.target` files):

```text
Target Mapping:
  poweroff.target    <─── [Runlevel 0] (Halt / Shutdown)
  rescue.target      <─── [Runlevel 1] (Single-User Maintenance)
  multi-user.target  <─── [Runlevel 3] (Multi-User CLI / Server Default)
  graphical.target   <─── [Runlevel 5] (Multi-User GUI / Desktop Default)
  reboot.target      <─── [Runlevel 6] (Reboot)
```

| systemd Target | SysV Runlevel | Purpose |
| :--- | :--- | :--- |
| **`poweroff.target`** | `0` | Shuts down and powers off the hardware. |
| **`rescue.target`** | `1` / `S` | Single-user root shell with basic filesystems mounted (no network). |
| **`multi-user.target`** | `2`, `3`, `4` | Full multi-user command-line interface (standard for servers). |
| **`graphical.target`** | `5` | Multi-user environment with graphical display manager (GDM/LightDM). |
| **`reboot.target`** | `6` | Gracefully terminates services and reboots the system. |
| **`emergency.target`** | *None* | Minimal emergency shell (root filesystem mounted read-only). |

---

## 4. Hands-on Service Management with `systemctl`

The **`systemctl`** command is your primary control tool for managing services, targets, and system power states.

> [!NOTE]
> When referring to service units in `systemctl` commands, the `.service` extension is optional (e.g., `apache2` implies `apache2.service`). Note that the Apache service is named **`apache2`** on Debian/Ubuntu and **`httpd`** on RHEL/Fedora.

### 1. Real-Time Runtime Control

```bash
# Start a service immediately
$ sudo systemctl start apache2

# Stop a running service
$ sudo systemctl stop apache2

# Restart a service (stop and start again)
$ sudo systemctl restart apache2

# Reload configuration without dropping active connections
$ sudo systemctl reload apache2
```

### 2. Boot-Time Autostart Configuration

```bash
# Enable a service to start automatically at boot
$ sudo systemctl enable apache2

# Disable a service from starting automatically at boot
$ sudo systemctl disable apache2

# Check if a service is enabled for automatic boot
$ systemctl is-enabled apache2

# Mask a service (links to /dev/null, preventing manual OR automatic start)
$ sudo systemctl mask apache2

# Unmask a previously masked service
$ sudo systemctl unmask apache2
```

### 3. Monitoring Service Health & Status

```bash
$ sudo systemctl status apache2
```

**Example Status Output Breakdown**:
```text
● apache2.service - The Apache HTTP Server
     Loaded: loaded (/lib/systemd/system/apache2.service; enabled; vendor preset: enabled)
     Active: active (running) since Mon 2026-08-18 10:15:30 UTC; 2h 14min ago
       Docs: https://httpd.apache.org/docs/2.4/
   Main PID: 1842 (apache2)
      Tasks: 55 (limit: 4642)
     Memory: 24.5M
        CPU: 1.240s
     CGroup: /system.slice/apache2.service
             ├─1842 /usr/sbin/apache2 -k start
             ├─1844 /usr/sbin/apache2 -k start
             └─1845 /usr/sbin/apache2 -k start

Aug 18 10:15:30 web01 systemd[1]: Starting The Apache HTTP Server...
Aug 18 10:15:30 web01 systemd[1]: Started The Apache HTTP Server.
```

- **Loaded**: Shows path to unit file and whether it is `enabled` for boot.
- **Active**: Current runtime state (`active (running)`, `inactive (dead)`, or `failed`).
- **Main PID**: The primary process ID of the daemon.
- **CGroup**: The cgroup tree displaying all child processes managed by this unit.
- **Log Snippet**: Real-time recent entries pulled directly from `systemd-journald`.

### 4. Target & Boot State Commands

```bash
# View the current default boot target (e.g., multi-user.target or graphical.target)
$ systemctl get-default

# Set the system to boot into text-only server mode by default
$ sudo systemctl set-default multi-user.target

# Set the system to boot into GUI desktop mode by default
$ sudo systemctl set-default graphical.target

# Switch to a target immediately on the live system (without rebooting)
$ sudo systemctl isolate rescue.target
```

---

## 5. `systemctl` Quick Reference Cheat Sheet

| Task | Command |
| :--- | :--- |
| **Check service state** | `systemctl status <unit>` |
| **Start / Stop service** | `sudo systemctl start <unit>` / `sudo systemctl stop <unit>` |
| **Restart / Reload** | `sudo systemctl restart <unit>` / `sudo systemctl reload <unit>` |
| **Enable / Disable on boot** | `sudo systemctl enable <unit>` / `sudo systemctl disable <unit>` |
| **List all running services** | `systemctl list-units --type=service --state=running` |
| **List failed services** | `systemctl --failed` |
| **View logs for a service** | `journalctl -u <unit> -e` |
| **Reboot system** | `systemctl reboot` (or `sudo reboot`) |
| **Power off system** | `systemctl poweroff` (or `sudo poweroff`) |