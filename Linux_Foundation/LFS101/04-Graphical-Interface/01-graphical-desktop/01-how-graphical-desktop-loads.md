# How the Graphical Desktop Loads

## 1. The Display Manager

When a Linux system boots into graphical mode, the first thing you see is the **greeter** (login screen), presented by the **display manager**. The display manager is the service responsible for authenticating users and starting their graphical session.

| Desktop Environment | Display Manager | Notes |
| :--- | :--- | :--- |
| GNOME (Ubuntu, Fedora, RHEL) | **GDM3** (GNOME Display Manager) | Default on all GNOME-based distributions covered in this course |
| KDE Plasma | **SDDM** (Simple Desktop Display Manager) | Default on modern KDE installations |

> [!NOTE]
> Older documentation may still reference **KDM** as KDE's display manager. KDM has been discontinued and replaced by SDDM on all current distributions.

---

## 2. The Display Server: X11 vs. Wayland

Underneath the display manager sits the **display server** — the software layer that handles communication between your hardware and the graphical applications running on top of it.

```text
+-------------------------------------------------------------+
|                  GRAPHICAL SESSION STACK                    |
+-------------------------------------------------------------+
|  [ Display Manager ]   e.g. GDM3, SDDM                      |
|         |  authenticates user, starts session               |
|         v                                                   |
|  [ Display Server ]    e.g. Wayland (or X11)                |
|         |  manages input, rendering, hardware access        |
|         v                                                   |
|  [ Desktop Environment ]  e.g. GNOME, KDE Plasma             |
+-------------------------------------------------------------+
```

### X11 (X Window System)
- Originated in the mid-1980s and has been a core component of Linux desktops since the kernel's inception in the early 1990s.
- Served the ecosystem reliably for decades, but its aging design increasingly struggles with modern security, performance, and hardware demands.

### Wayland
- The modern successor to X11, with a cleaner, more secure architecture.
- **Default** on most current distributions, including Ubuntu 22.04+, Fedora, and RHEL.
- Older releases (Ubuntu 18.04, CentOS 7) still default to X11, which continues to function reliably.
- For everyday use, the switch from X11 to Wayland is largely transparent — the desktop looks and behaves the same. The real differences are architectural: improved security, better support for high-resolution displays and fractional scaling, and more responsive input handling.

> [!NOTE]
> Some older applications were written specifically for X11 and don't run natively under Wayland. **XWayland**, a compatibility layer bundled automatically with modern Wayland installations, runs these applications inside a Wayland session with no extra configuration. In practice, the vast majority of applications work without issue.

Ubuntu 24.04 still lets you choose between Wayland and X11 at the login screen, but newer GNOME releases are removing that option altogether. X11 is being phased out across the ecosystem, and Wayland is now the established standard on current distributions.

---

## 3. Starting the Desktop Manually

If the graphical desktop doesn't start automatically, it can be launched from a text console by starting the display manager directly:

| Method | Command | Result |
| :--- | :--- | :--- |
| Start the display manager (Debian/Ubuntu) | `sudo systemctl start gdm3` | Presents the normal login screen |
| Start the display manager (Fedora/RHEL) | `sudo systemctl start gdm` | Presents the normal login screen |
| Launch a session directly | `startx` | Bypasses the login screen entirely; less common on modern installs, but a useful fallback when the display manager won't start |
