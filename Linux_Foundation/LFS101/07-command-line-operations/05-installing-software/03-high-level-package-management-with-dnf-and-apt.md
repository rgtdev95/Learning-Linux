# High-Level Package Management with dnf and apt

## 1. `dnf` Demo (Fedora/RHEL/CentOS)

Search for packages related to a topic — e.g., everything with "bzip2" in the name:

```bash
$ dnf list bzip2
```

This shows both installed packages (the base library, development libraries, a Perl compression module) and available packages (development libraries, and utilities such as `lbzip2`).

Install a package:

```bash
$ sudo dnf install lbzip2
```

`dnf` shows the download size and installed size, then prompts for confirmation.

> [!NOTE]
> `dnf`'s confirmation prompt defaults to **No** (shown capitalized as `N`) — pressing Enter without typing anything answers no. Type `y` explicitly to proceed.

Remove a package:

```bash
$ sudo dnf remove lbzip2
```

`dnf` reports what it found, how much space will be freed, and again requires an explicit `y` to confirm.

> [!NOTE]
> Had there been dependencies, `dnf` would have resolved and handled them automatically, the same as during installation. There's no graphical package manager on a minimal CentOS install by default, but most users find the command line just as fast and easy for these operations.

## 2. `apt` Demo (Debian/Ubuntu)

Search the local package cache for packages matching a name:

```bash
$ apt-cache search wget2
```

This searches the locally cached package list (periodically refreshed from the repositories), returning results such as a library package, the `wget2` command itself, and a development package.

Install a package:

```bash
$ sudo apt-get install wget2-dev
```

`apt-get` reports any additional dependencies needed — in this case, the base `wget2` package itself — along with the total download and installed size, then prompts to continue.

> [!NOTE]
> Many Linux command-line prompts capitalize the default answer (e.g., `[Y/n]`) — pressing Enter without typing anything accepts that capitalized default.

Remove a package:

```bash
$ sudo apt-get remove wget2
```

`apt-get` checks dependencies again before removing — since `wget2-dev` depends on `wget2`, both are removed together, along with a note about any packages that were "automatically installed" and are no longer required.

> [!NOTE]
> These are the core day-to-day operations for command-line package management under a Debian-based system: searching for a package, checking what's inside it, installing it, and removing it.
