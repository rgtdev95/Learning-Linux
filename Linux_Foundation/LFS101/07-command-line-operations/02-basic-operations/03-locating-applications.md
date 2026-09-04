# Locating Applications (Command Line)

## 1. Where Programs Live

Depending on a distribution's policy, programs and software packages can be installed in various directories. In general, executable programs and scripts are located in standard paths:

| Location | Typical Contents |
| :--- | :--- |
| `/bin`, `/usr/bin` | Standard user executables |
| `/sbin`, `/usr/sbin` | System administration executables |
| `/opt` | Third-party or self-contained application installs |
| `/usr/local/bin`, `/usr/local/sbin` | Manually installed software |
| `~/bin` (e.g., `/home/student/bin`) | A user's own local binaries |

> [!NOTE]
> As covered in [A Closer Look at the Filesystem Hierarchy](../../03-linux-basics-and-system-startup/understanding-linux-file-system/04-closer-look-at-the-filesystem-hierarchy.md), on modern systemd-based distributions (including Ubuntu 24.04, recent CentOS, and openSUSE), `/bin` and `/sbin` are now simply symbolic links into their `/usr` counterparts — the "usr-merge." So `/bin/diff` and `/usr/bin/diff` refer to the same file.

## 2. Locating a Program: `which`, `whereis`, `type`

Several utilities can locate these programs.

### `which`

Shows the full path to a program based on the current `$PATH` environment variable. Useful for confirming exactly which version of a command will run.

```bash
$ which diff
/usr/bin/diff
```

### `whereis`

A broader alternative — locates the binary, its source code, and its manual pages.

```bash
$ whereis diff
diff: /usr/bin/diff /usr/share/man/man1/diff.1.gz /usr/share/man/man1p/diff.1p.gz
```

### `type`

A shell built-in that reports what a command actually *is* — a program on disk, a shell built-in, an alias, or a function — which can clear up confusion when a command behaves unexpectedly.

```bash
$ type diff
diff is /usr/bin/diff

$ type ll
ll is aliased to 'ls -l --color=auto'
```

> [!NOTE]
> `type diff` shows that `diff` is a real program on disk (`/usr/bin/diff`), while `type ll` reveals that `ll` isn't a program at all — it's an alias expanding to `ls -l --color=auto`. This is something `which` alone can't always tell you.
