# Virtual Terminals

A **Virtual Terminal (VT)** is a full-screen text session that runs entirely outside the graphical environment. Multiple VTs can be active simultaneously, but only one is visible at a time.

One VT (usually VT1 or VT7) is reserved for the graphical session, with the remaining VTs available for text logins. This is particularly useful if the graphical desktop becomes unresponsive: switching to a VT allows troubleshooting without a full reboot.

| Action | Shortcut |
| :--- | :--- |
| Switch to a VT from the graphical session | `Ctrl+Alt+F(n)` — e.g., `Ctrl+Alt+F3` for VT3 |
| Switch between VTs from within another VT | `Alt+F(n)` |

> [!NOTE]
> Desktop environments and graphical tools vary between distributions, but the command line stays largely consistent. Learn it on one system, and most of that knowledge carries over directly to the next.

> [!NOTE]
> There isn't a direct equivalent in Windows or macOS. The closest comparison is Windows Safe Mode, though VTs are considerably lighter-weight and quicker to access.
