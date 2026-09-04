# The `find` Utility

`find` is an extremely useful and frequently used utility in the daily life of a Linux system administrator. It recurses down the filesystem tree from a given directory (or set of directories) and locates files that match specified conditions. If no starting directory is given, `find` begins from the present working directory.

> [!NOTE]
> Administrators commonly use `find` to scan for large core files more than several weeks old and remove them, or to clear out outdated files in `/tmp` and other volatile directories (such as `/var/cache/`) that haven't been accessed recently. Many distributions run shell scripts via `cron` to perform this kind of housekeeping automatically.

## 1. Basic Usage

Given only a starting directory and no other conditions, `find` lists all files in that directory and its subdirectories. Common options to narrow results:

| Option | Effect |
| :--- | :--- |
| `-name` | List only files whose name matches a given pattern |
| `-iname` | Same as `-name`, but case-insensitive |
| `-type` | Restrict results to a type — `d` (directory), `l` (symbolic link), `f` (regular file) |

```bash
# Files and directories named gcc under /usr
$ find /usr -name gcc

# Only directories named gcc
$ find /usr -type d -name gcc

# Only regular files named gcc
$ find /usr -type f -name gcc
```

## 2. Running Commands on Matches: `-exec` and `-ok`

`-exec` runs a command on each file that matches the search. To find and remove all files ending in `.swp`:

```bash
$ find -name "*.swp" -exec rm {} ';'
```

The `{}` is a placeholder replaced with each matching filename, and the command runs once per match. End the command with either `';'` (including the quotes) or `\;` — both forms work.

> [!WARNING]
> Use straight single quotes (`'`), not curly/"smart" quotes, or the command fails if copied from a document into the terminal.

`-ok` works just like `-exec`, but prompts for confirmation before running the command on each file — a safe way to preview results before something potentially destructive:

```bash
$ find -name "*.swp" -ok rm {} ';'
```

## 3. Finding Files by Time and Size

```bash
$ find / -ctime 3
```

`-ctime` refers to when a file's inode metadata (ownership, permissions, etc.) last changed — not the same as its creation time. Standard `find` options work with change, access, and modification times, not creation time. Search by last-accessed time with `-atime`, or last-modified time with `-mtime`. The number is a count of days: `n` (exactly that many days), `+n` (more than that many days), or `-n` (fewer than that many days). Equivalent options exist in minutes: `-cmin`, `-amin`, `-mmin`.

```bash
$ find / -size 0
```

By default, size is measured in 512-byte blocks. Other units: `c` (bytes), `k` (kilobytes), `M` (megabytes), `G` (gigabytes). As with time, sizes can be written as `n`, `+n`, or `-n`.

```bash
# Files larger than 10 MB, running a command on each
$ find / -size +10M -exec command {} ';'
```

> [!TIP]
> Starting a search at `/` scans the entire filesystem and, as a regular user, may produce many "Permission denied" messages. When practicing, start from a smaller directory (such as the home directory or `/tmp`) for faster, cleaner results.

## 4. Demo Walkthrough

This demo explores `/var/log` (using `sudo` since some files there are root-only):

1. `sudo find .` — lists every file under `/var/log` and its subdirectories; a long list.
2. `find . -type d` — narrows that to directory names only.
3. `find . -type d -maxdepth 1` — limits the depth of the search, avoiding deeply nested subdirectories that clutter the view. `-maxdepth` accepts any number depending on how far down the tree you want to go.
4. `find . -type f -exec grep -H log {} \;` — finds regular files and runs `grep -H log` on each match, printing every line containing the word "log" across all of them. The `{}` is replaced with the matched filename, and the command is terminated with `\;` (or `';'`) so the shell passes the semicolon through to `find` rather than treating it as the end of the whole command line.
5. `find . -type f -ls` — a shortcut for running a long listing (`ls -l`) on every match via `-exec`, but built into `find` directly, with extra detail such as inode numbers.
6. `find . -type f -size 0 -ls` — finds zero-size files and lists them to confirm.
7. `find . -newer /var/log/btmp` — finds all files modified more recently than a given reference file (here, `/var/log/btmp`), useful for finding everything changed since a known event.

> [!TIP]
> `find` has a huge number of options. Reading the full man page in one sitting can be overwhelming — instead, learn one new option at a time as the need comes up, and it will accumulate naturally.
