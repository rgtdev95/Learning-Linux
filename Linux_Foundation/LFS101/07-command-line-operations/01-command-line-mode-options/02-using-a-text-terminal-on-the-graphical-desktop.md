# Using a Text Terminal on the Graphical Desktop

## 1. Understanding Terminal Emulators

A **terminal emulator** opens a window that behaves like a standalone text-only terminal, even while running a full graphical desktop. Most terminal emulators support multiple sessions through tabs, similar to a web browser.

| Distribution | Default Terminal Emulator |
| :--- | :--- |
| Ubuntu, openSUSE (GNOME) | `gnome-terminal` |
| CentOS (GNOME) | `gnome-terminal`, unless KDE is installed, in which case `konsole` |

Other terminal emulators worth knowing: `xterm`, `konsole`, `terminator`.

## 2. Launching Terminal Windows

Modern GNOME Shell (used by Ubuntu, CentOS, and openSUSE) no longer has the older-style Applications menu, so don't expect to find one. Current methods include:

- Select **Activities** in the top-left corner, or press the **Super**/Windows key, then type "terminal" and press Enter.
- On Ubuntu, **Ctrl+Alt+T** opens a terminal directly — the quickest method, worth learning early.
- Right-clicking the desktop background and selecting **Open in Terminal** also works on most systems, with no additional setup required.

> [!TIP]
> Once you've located your terminal, it's worth pinning it to the favorites bar, since you'll be using it frequently throughout the course.
