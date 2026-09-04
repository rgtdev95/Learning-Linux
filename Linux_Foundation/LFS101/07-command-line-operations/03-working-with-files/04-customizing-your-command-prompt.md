# Customizing Your Command Prompt

The `PS1` variable defines the command-line prompt. Most distributions set `PS1` to a sensible default, which works well in most cases. However, it can be customized to show information such as the username and hostname:

```
student@r9 $
```

This is useful when working in multiple roles and wanting a constant reminder of who you are and which machine you're on.

## Prompt Escape Sequences

The prompt is built from backslash escape sequences, each standing for a piece of information:

| Escape Sequence | Description |
| :--- | :--- |
| `\u` | Current username |
| `\h` | Hostname, up to the first `.` |
| `\w` | Current working directory (`~` for home) |
| `\$` | Displays `#` if root (UID 0), `$` for all other users |

Put those together and set `PS1` to `\u@\h \$` — note the trailing space, which keeps the cursor from sitting directly against the `$`:

```bash
$ PS1='\u@\h \$ '
student@r9 $
```

> [!WARNING]
> Use single quotes when assigning this. Inside double quotes, bash processes the backslash and stores `\$` as a plain `$`, which loses the dynamic behavior — the prompt would always show `$`, even for root. Single quotes store the literal `\$` sequence, so the prompt correctly renders as `$` for normal users and `#` for root:
> ```bash
> $ echo $PS1
> \u@\h \$
> ```

By convention, most systems are set up so the root user has a pound sign (`#`) as their prompt — exactly the behavior the `\$` sequence provides automatically.

> [!NOTE]
> Setting `PS1` this way only affects the current shell session. To make the change permanent, add the `PS1` line to a shell startup file such as `~/.bashrc`.
