# The Command Line

## 1. Anatomy of a Command

Most commands entered at the shell prompt break down into three parts:

| Part | Description |
| :--- | :--- |
| **Command** | The specific program, utility, or script being executed |
| **Options** | Switches, typically prefixed with a single dash (`-`) for short forms or a double dash (`--`) for long forms, that alter or expand how a command behaves (e.g., `-p` or `--print`) |
| **Argument** | The target of the command — the exact file, path, or data it should process |

## 2. `sudo`

`sudo` ("switch user and do") allows a user to run commands with another user's privileges (typically root's) without logging in as that user directly.

> [!NOTE]
> For Windows users, `sudo` is roughly equivalent to "Run as Administrator." On macOS, it's the same `sudo` command, since macOS shares Unix ancestry with Linux.

Default configuration varies by distribution:

| Distribution | Default sudo Behavior |
| :--- | :--- |
| **Ubuntu** | Configured automatically during installation — the first user account created is granted sudo access immediately. Direct `su` login and the root account are disabled by default, as a security measure. |
| **CentOS / openSUSE** | Typically set a root password during installation; sudo access for other users must be configured manually. |

## 3. Setting Up and Running sudo

On most modern desktop installations of Ubuntu, `sudo` is configured automatically. The steps below are only needed when adding a new user, or on a distribution (like some CentOS/openSUSE installations) where sudo access must be explicitly granted.

### Become root

On Ubuntu, since the root account has no password by default, use `sudo -i` or `sudo su` instead of plain `su`. On CentOS/openSUSE, where a root password was set at install time, `su` works directly:

```bash
$ su
Password:
#
```

> [!NOTE]
> No characters are displayed while typing the password — this is expected behavior.

### Grant sudo access

Use `visudo` to edit the configuration, since it validates syntax before saving.

> [!WARNING]
> Editing the sudoers file directly (for instance, with `echo "..." > /etc/sudoers.d/username`) skips that validation — a typo can lock out administrative access system-wide, with no easy recovery short of booting into recovery mode.

```bash
# visudo -f /etc/sudoers.d/username
```

Then add:

```
username ALL=(ALL) ALL
```

On Ubuntu, run this from an existing admin account instead:

```bash
$ sudo visudo -f /etc/sudoers.d/username
```

> [!NOTE]
> Replace `username` with the actual account name.

### Set file permissions (if required)

Some systems require specific security permissions on the configuration file:

```bash
# chmod 440 /etc/sudoers.d/username
```

Once configured, `sudo` prompts for the user's own password — not root's — the first time it's used in a session, and periodically thereafter.

> [!NOTE]
> `su` versus `sudo`, and the differing philosophies behind each distribution's approach, are covered in more depth later in the security section.

## 4. Switching Between the GUI and the Command Line

On Linux, the graphical desktop is optional rather than a fixed part of the system. Ubuntu, CentOS, and openSUSE all offer both a full desktop installation and a GUI-free server edition.

Production servers typically run without a GUI, since fewer components generally means a leaner, more secure, and easier-to-maintain system.

> [!NOTE]
> This differs from Windows Server, which has historically relied more heavily on a GUI, though a GUI-free "Server Core" option is now available. macOS does not offer a comparable GUI-free option at all.
