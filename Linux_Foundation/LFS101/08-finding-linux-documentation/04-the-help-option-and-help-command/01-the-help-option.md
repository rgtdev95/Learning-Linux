# The `--help` Option

Another important source of Linux documentation is the `--help` option.

Most commands print a short usage summary when `--help` is added after the command name:

```bash
$ ls --help
```

This lists what the command does and the options it accepts. Unlike `man` and `info`, `--help` prints its output directly to the terminal and returns straight to the prompt — there's no pager to scroll through or quit. That makes it the fastest way to jog your memory about a command's options.

> [!WARNING]
> Many commands accept a short `-h` option, and while it sometimes means "help," that's not always true. For several common commands (such as `ls`, `df`, and `du`), `-h` stands for "human-readable" output sizes. When documentation is needed, always reach for the long form, `--help`, which is far more consistent across commands.
