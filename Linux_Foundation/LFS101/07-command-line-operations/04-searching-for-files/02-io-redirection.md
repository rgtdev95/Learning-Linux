# I/O Redirection

Through the command shell, the three standard file streams can be redirected — getting input from a file or another command instead of the keyboard, and sending output and errors to files or using them as input for other commands.

## Redirecting Input and Output

Suppose a program called `do_something` reads from `stdin` and writes to `stdout` and `stderr`. Change its input source with `<`:

```bash
$ do_something < input-file
```

Send the output to a file with `>`:

```bash
$ do_something > output-file
```

Both at the same time:

```bash
$ do_something < input-file > output-file
```

> [!NOTE]
> Because `stderr` is separate from `stdout`, error messages still appear in the terminal in the example above — only the normal output was redirected.

## Redirecting stderr

To redirect `stderr` to its own file, use its file descriptor number (`2`) immediately before `>`:

```bash
$ do_something 2> error-file
```

> [!NOTE]
> By the same logic, `do_something 1> output-file` is the same as `do_something > output-file`. When no descriptor number is given before `>`, the shell assumes `1` (stdout).

## Combining stdout and stderr

The notation `2>&1` sends file descriptor 2 (stderr) to wherever file descriptor 1 (stdout) is currently going. To capture everything in one file:

```bash
$ do_something > all-output-file 2>&1
```

> [!WARNING]
> Order matters here: `>` sets where stdout goes first, and `2>&1` then points stderr at that same destination. Writing it the other way around (`2>&1 > all-output-file`) will **not** combine them, because the shell reads redirections from left to right.

`bash` also permits a shorter form that does the same thing:

```bash
$ do_something >& all-output-file
```
