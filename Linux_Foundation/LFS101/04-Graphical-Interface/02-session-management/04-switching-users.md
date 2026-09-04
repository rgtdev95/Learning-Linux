# Switching Users

## 1. Linux Is a True Multi-User System

Linux was designed from the ground up to support multiple users, and it does so properly — more than one person can have an active session on the same system simultaneously, each with their own user account, password, home directory, personal files, and settings. Those sessions are kept completely separate, protecting each user's data from being accessed or modified by others.

> [!NOTE]
> This is worth appreciating coming from a typical home Windows or macOS setup, where multi-user support exists but is rarely a central design consideration. On Linux, it's fundamental to how the system works — and that has practical implications even on a single-user machine: the same permission model that makes multi-user operation secure also protects the system from accidental damage and unauthorized changes.

## 2. How User Switching Works

Each user can log in, run applications, and maintain an active session entirely independently of any other user on the system:

- Users can take turns on the same machine while keeping their respective sessions intact — applications do not need to be closed when handing over the computer.
- Sessions can also run simultaneously, with users connected through the network or through separate terminal sessions, not just at the physical console.

## 3. Switching Users by Desktop Environment

| Desktop Environment | How to Switch |
| :--- | :--- |
| **GNOME** (Ubuntu, Fedora, openSUSE) | System menu (upper-right corner) → **Switch User**, either directly or nested inside a user account menu, depending on the distribution |
| **KDE Plasma** | Application launcher, or the user icon in the system tray → **Switch User** |
| **Cinnamon** (Linux Mint) | Menu under your username, or the system tray area |

In every case, selecting **Switch User** returns to the login screen while your current session keeps running in the background — the other user logs in to their own session without affecting yours. Returning to your own session is simply a matter of selecting your account at the login screen and entering your password again.

## 4. Why This Matters Beyond Switching

Even if you are the only person using a system, understanding how user accounts work is important. Each account operates within a defined set of permissions that determines what it can read, write, and execute. This structure is what prevents a misbehaving application or an accidental command from causing system-wide damage — it's the foundation for a lot of what comes later in the course: user accounts, permissions, and the relationship between regular users and the administrator account.
