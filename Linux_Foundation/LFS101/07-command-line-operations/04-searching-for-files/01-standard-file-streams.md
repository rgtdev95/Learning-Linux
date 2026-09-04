# Standard File Streams

When commands execute, three standard file streams (or descriptors) are always open by default: standard input, standard output, and standard error.

| Name | Abbreviation | File Descriptor | Default Source/Destination |
| :--- | :--- | :--- | :--- |
| Standard input | stdin | 0 | Keyboard |
| Standard output | stdout | 1 | Terminal |
| Standard error | stderr | 2 | Terminal |

Usually, `stdin` comes from the keyboard, while `stdout` and `stderr` are both printed on the terminal. Each of these can be redirected elsewhere:

- **stdin** can be supplied from a file, or from the output of a previous command through a pipe.
- **stdout** is often redirected into a file, so a command's results are saved rather than displayed.
- **stderr** is often redirected to a separate error-logging file, keeping error and warning messages out of the normal output.

> [!NOTE]
> Because `stderr` is used only for error and warning messages, a command that runs successfully typically writes nothing to it.

## File Descriptors

In Linux, all open files are represented internally by **file descriptors** — numbers the system uses to track each open file, starting at zero. As shown above, `stdin` is file descriptor `0`, `stdout` is `1`, and `stderr` is `2`. If a command opens additional files beyond these three, they're assigned the next available numbers, starting at `3` and increasing from there.
