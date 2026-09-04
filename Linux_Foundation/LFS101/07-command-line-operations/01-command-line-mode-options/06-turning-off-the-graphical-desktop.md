# Turning Off the Graphical Desktop

Linux distributions can start and stop the graphical desktop in various ways; the exact method differs somewhat between distributions and versions.

## 1. Switching Targets with `systemctl`

For newer systemd-based distributions — including Ubuntu, CentOS, and openSUSE — the system is managed through **targets** rather than the older SysV runlevel numbers.

```bash
$ sudo systemctl isolate multi-user.target
```

This switches the system to text-only mode (equivalent to the old runlevel 3).

```bash
$ sudo systemctl isolate graphical.target
```

This brings the graphical desktop back (equivalent to the old runlevel 5).

## 2. The Legacy `telinit` Command

Most distributions will also still accept the older `telinit` command, since runlevel requests are transparently translated into the equivalent systemd target:

```bash
$ sudo telinit 3
$ sudo telinit 5
```

> [!NOTE]
> `telinit` still works and may show up in older scripts or documentation, but `systemctl` is the preferred approach on modern systems, since it operates directly on systemd's targets rather than through a compatibility layer.

## 3. Stopping Just the Display Manager

Instructions may instead point to stopping or starting just the display manager service (`gdm` on Ubuntu and openSUSE GNOME systems) rather than switching the whole system's target:

```bash
$ sudo systemctl stop gdm
$ sudo systemctl start gdm
```

> [!NOTE]
> This is a related but slightly different action: it stops the display manager itself rather than transitioning the entire system between text-only and graphical states. The visible result on a typical desktop machine often looks similar either way, but the two aren't strictly interchangeable.
