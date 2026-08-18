# Stages 5 & 6: System Initialization, Virtual Terminals & Logins

## 1. System Initialization: The Role of `systemd` (PID 1)

When the kernel executes `/sbin/init` (which on modern distributions is a symlink to `/lib/systemd/systemd`), **systemd** becomes **Process ID 1 (PID 1)**—the ancestor of all processes in user space.

```text
[ Kernel executes /sbin/init (PID 1) ]
                  │
                  ▼
[ systemd Initializes Core System Services ]
  ├── Mounts local filesystems listed in /etc/fstab
  ├── Configures hostname, network interfaces, and firewall
  ├── Starts system daemons (sshd, cron, NetworkManager, dbus)
  └── Activates Default Target State
        ├── multi-user.target (Headless Server / Command Line)
        └── graphical.target  (Desktop / Display Manager)
                  │
                  ▼
[ Login Management Subsystem ]
  ├── Spawns getty / agetty processes on Virtual Terminals (tty1 - tty6)
  └── Starts Display Manager (GDM / LightDM / SDDM) if GUI is configured
```

---

## 2. Virtual Terminals (TTYs)

Linux is a multi-user system capable of running multiple independent interactive terminal sessions simultaneously. These sessions are known as **Virtual Terminals** or **Virtual Consoles** (represented by device nodes `/dev/tty1` through `/dev/tty6`).

```text
+-------------------------------------------------------------------------+
|                      VIRTUAL TERMINALS (CONSOLES)                       |
+-------------------------------------------------------------------------+
|  TTY1: Text Login   TTY2: Text/GUI    TTY3: Text Login  TTY4: Text Login|
|  TTY5: Text Login   TTY6: Text Login  TTY7: GUI (Traditional X11)       |
+-------------------------------------------------------------------------+
```

### Switching Shortcuts

| Starting Environment | Target Destination | Key Combination |
| :--- | :--- | :--- |
| **Inside a Text Console (TTY)** | Switch to another Text Console (e.g., TTY 3) | `Alt + F3` |
| **Inside a Graphical Desktop (GUI)** | Switch to a Text Console (e.g., TTY 2 or 3) | `Ctrl + Alt + F2` (or `F3` through `F6`) |
| **Inside a Text Console (TTY)** | Return to the Graphical Desktop | `Alt + F1`, `Alt + F2`, or `Alt + F7` *(depends on distro)* |

> [!TIP]
> On modern distros using Wayland (such as Ubuntu, Fedora, and RHEL), the graphical login screen typically runs on **TTY 1**, and the active user desktop session runs on **TTY 2**. On older X11 setups, the GUI traditionally resided on **TTY 7**.

---

## 3. The Text-Mode Login Lifecycle

When a text console is initialized:

```text
+-----------------------------------------------------------------------+
| 1. agetty / getty                                                     |
|    └─ Opens the TTY port, sets terminal parameters, and displays the  |
|       "login:" prompt.                                                |
+-----------------------------------┬-----------------------------------+
                                    │ (User types username)
                                    ▼
+-----------------------------------------------------------------------+
| 2. /bin/login                                                         |
|    └─ Prompts for password (hidden, no echo).                         |
|    └─ Validates credentials against /etc/passwd & /etc/shadow using   |
|       PAM (Pluggable Authentication Modules).                         |
+-----------------------------------┬-----------------------------------+
                                    │ (Authentication Successful)
                                    ▼
+-----------------------------------------------------------------------+
| 3. Spawns User Shell                                                  |
|    └─ Sets environment variables (HOME, USER, PATH, SHELL).           |
|    └─ Executes the default shell specified in /etc/passwd             |
|       (e.g., /bin/bash, /bin/zsh).                                    |
|    └─ Reads startup profiles (~/.bash_profile, ~/.bashrc).            |
+-----------------------------------┬-----------------------------------+
                                    │
                                    ▼
+-----------------------------------------------------------------------+
| 4. Interactive Shell Prompt Ready                                     |
|    user@hostname:~$                                                   |
+-----------------------------------------------------------------------+
```

---

## 4. The Shell & The Interactive Prompt

Once logged in, the user interacts with the system through the **Shell** (the command interpreter, predominantly **GNU Bash**).

### Understanding the Prompt Symbol
- **`$` (Dollar Sign)**: Indicates a **standard, non-privileged user account** (e.g., `ron@linuxbox:~$`).
- **`#` (Hash / Pound Sign)**: Indicates the **administrative superuser (`root`)** account (e.g., `root@linuxbox:~#`).

### The REPL Execution Cycle
The shell operates in a continuous loop:
```text
[ Read ]   ──> User types a command (e.g., ls -la) and presses [Enter]
   │
[ Eval ]   ──> Shell parses aliases, expands variables, and asks kernel to execute
   │
[ Print ]  ──> Output or error stream is rendered to the terminal screen
   │
[ Loop ]   ──> Shell reprints the prompt ($) and waits for next instruction
```
