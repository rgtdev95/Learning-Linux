# Pipes

The UNIX/Linux philosophy favors many simple, short programs working together to produce complex results, rather than one large program with many options and modes of operation. **Pipes** make this possible: a pipe takes the output of one command and feeds it directly in as the input of the next.

This works by connecting the `stdout` of one command to the `stdin` of the next — the two standard streams covered previously. Create a pipe with the vertical-bar symbol (`|`) between commands:

```bash
$ command1 | command2 | command3
```

This is called a **pipeline**, and it lets Linux combine the actions of several commands into one:

```bash
$ ls | wc -l
```

Here, `ls` lists the files in the current directory, and its output is piped into `wc -l`, which counts the lines — giving a count of the files, without either command needing to save anything to a file in between.

## Why Pipelines Are Efficient

- **The commands run at the same time.** Each command starts processing data as soon as it arrives, rather than waiting for the previous command to finish completely. On systems with multiple CPUs or cores, this makes much better use of the available computing power and gets work done faster.
- **No temporary files are needed.** Because data flows directly from one command to the next, there's no need to save intermediate results to disk between stages — saving disk space and avoiding disk I/O, often the slowest part of getting a task done.
