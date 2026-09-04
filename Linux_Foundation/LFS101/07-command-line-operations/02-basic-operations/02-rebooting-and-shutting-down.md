# Rebooting and Shutting Down (Command Line)

## 1. The `shutdown` Command

The preferred method for shutting down or rebooting the system is the `shutdown` command. It sends a warning message to logged-in users and prevents new logins before the operation takes place.

> [!WARNING]
> Always shut down properly. An improper shutdown — cutting power directly — can result in data loss or system damage.

| Command | Effect |
| :--- | :--- |
| `shutdown -h` | Halts the system (powers off). `halt` and `poweroff` are often aliases for this action. |
| `shutdown -r` | Reboots the system. `reboot` is an alias for this action. |

> [!NOTE]
> Both `shutdown` and `reboot` require superuser (root) access.
>
> This is the command-line equivalent of the GUI Power Off/Restart flow covered in [Shutting Down and Restarting](../../04-graphical-interface/02-session-management/07-shutting-down-and-restarting.md).

## 2. Scheduling a Shutdown with a Notification

On a multi-user system, `shutdown` can notify everyone logged in before it acts, and can be scheduled for a specific time:

```bash
$ sudo shutdown -h 10:00 "Shutting down for scheduled maintenance."
```

This schedules a halt for 10:00, sending the quoted message to every logged-in user's terminal beforehand.
