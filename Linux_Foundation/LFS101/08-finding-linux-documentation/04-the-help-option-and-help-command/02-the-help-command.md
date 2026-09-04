# The `help` Command

When working in the bash shell, a handful of common commands — such as `cd`, `echo`, and `pwd` — are not separate programs located in `/bin` or `/usr/bin`. Instead, bash runs its own shell **built-in** versions. This is faster and lighter, since the shell doesn't have to launch a separate program to do the job. Occasionally, the built-in version behaves slightly differently from a standalone program of the same name.

Bash provides its own `help` command as the dedicated way to document these built-ins:

```bash
$ help          # lists all the built-in commands
$ help cd       # shows usage for a specific built-in, e.g. cd
```

> [!NOTE]
> Many built-ins also respond to `--help` directly (e.g., `cd --help`), but `help` is more reliable for two reasons: only `help` can list all the built-ins at once, and it still works in the occasional case where `--help` doesn't behave as expected — `echo --help`, for instance, simply prints the text "--help" rather than showing usage.

> [!NOTE]
> Coming from Windows, `--help` is much like adding `/?` after a command in the Command Prompt — a quick, inline usage reminder. macOS users will find terminal commands behave similarly to Linux, though some macOS built-ins rely more heavily on `man`.

> [!TIP]
> Unsure whether a command is a shell built-in or an external program? Use `type <command>` — for example, `type cd` vs. `type ls`.
