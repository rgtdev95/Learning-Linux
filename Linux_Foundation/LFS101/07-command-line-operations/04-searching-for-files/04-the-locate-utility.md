# The `locate` Utility

`locate` performs a search by taking advantage of a previously built database of files and directories on the system, matching all entries that contain a specified text string. Because it searches a database rather than scanning the disk directly, it's very fast, but it can sometimes return a very long list.

## Narrowing Results with `grep`

To get a shorter (and possibly more relevant) list, pipe the results through `grep` as a filter — it prints only the lines that contain one or more specified strings:

```bash
$ locate zip | grep bin
```

This lists all entries whose path contains both `zip` (matched by `locate`) and `bin` (matched by `grep`) — for example, `/usr/bin/gzip`. These strings can appear anywhere in the full path, not just in the filename.

## The `updatedb` Database

`locate` relies on a database created by a related utility, `updatedb`. Most Linux systems rebuild this database automatically on a schedule (commonly once a day) — meaning a file created very recently may not appear in `locate` results until the database is next updated. Update it manually at any time as root:

```bash
$ sudo updatedb
```

> [!NOTE]
> On some systems, `locate` isn't installed by default and may need to be added through the distribution's package manager. Many current distributions now ship `plocate`, a faster, drop-in replacement for the older `mlocate`. Both provide the same `locate` and `updatedb` commands, so the examples above work the same way regardless of which one a system uses.

## Wildcards and Matching Filenames

When the exact filename isn't known, wildcards can match filenames that contain specific characters. Wildcards are a feature of the shell itself — before a command runs, the shell expands the wildcard pattern into the list of matching filenames and passes them to the command. This is why wildcards work with almost any command, not just the ones shown here.

| Wildcard | Result |
| :--- | :--- |
| `?` | Matches any single character |
| `*` | Matches any string of characters (including none) |
| `[set]` | Matches any single character in the set — e.g., `[adf]` matches `a`, `d`, or `f` |
| `[!set]` | Matches any single character *not* in the set |

### Examples

```bash
# Using ? — filename is three letters, begins with "ba", ends in .out
$ ls ba?.out

# Using * — only the .out extension is known
$ ls *.out

# Using [set] — match file_a.out, file_b.out, or file_c.out only
$ ls file_[abc].out

# Using [!set] — match files where the character after "file_" is NOT a, b, or c
$ ls file_[!abc].txt
```

> [!NOTE]
> If a wildcard pattern matches no files, bash passes the pattern through unchanged — so the command receives the literal text (for example, `ls *.out` with no matches produces an error about a file named `*.out`).

## Demo: Wildcards in Practice

This demo explores wildcard expansion from `/var/log`:

- `du -sh a*` — summarizes disk usage for everything starting with `a`, including directories like `apt` and various log files.
- `du -sh a*log*` — narrows that to filenames starting with `a` that also contain "log" somewhere in the name.
- `du -sh a[p-z]*` — matches names starting with `a`, followed by a letter `p` through `z`, then anything else — skipping files like the "alternative" log files that don't fit that range.
- A pattern like `.?.` matches filenames containing a dot, a single character, another dot, and anything after — useful for finding rotated log files such as `name.1.log` or `name.gz`.

> [!WARNING]
> Be careful with wildcard expansion, known as **globbing**. The shell expands a pattern like `vmware*` into every matching filename *before* the command ever runs. For a command like `sudo apt-get install vmware*`, this means apt receives a long list of literal filenames (log files, etc.) instead of a single package name pattern — producing a wall of errors, since none of those are real package names.
>
> To pass a wildcard pattern to a command *unexpanded*, wrap it in quotes (single or double, as long as they match):
> ```bash
> $ sudo apt-get install "vmware*"
> ```
> This lets `apt-get` itself interpret the pattern against its own package list, rather than having the shell expand it against filenames first.
