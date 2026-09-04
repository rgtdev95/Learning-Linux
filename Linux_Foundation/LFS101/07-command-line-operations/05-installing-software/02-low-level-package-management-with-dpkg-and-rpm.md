# Low-Level Package Management with dpkg and rpm

## 1. `dpkg` Demo (Debian-Based)

This demo uses the Debian low-level packaging tool, `dpkg`.

List all packages installed on the system:

```bash
$ dpkg --list | less
```

Search for information on a specific package (e.g., `bzip2`):

```bash
$ dpkg --list | grep bzip2
```

This shows the version number, architecture (e.g., `amd64`), and description — in this case, a high-quality block-sorting file compressor, with better compression than `gzip` or the older `zip`.

List the files contained in a package:

```bash
$ dpkg --listfiles bzip2 | less
```

This shows executables under `/bin`, and documentation under `/usr/share/doc`, `/usr/share/man`, and similar paths.

Attempting to remove a package:

```bash
$ sudo dpkg --remove bzip2
```

> [!NOTE]
> This fails if other installed packages depend on it — in this demo, `dpkg-dev` (headers for programs that use `bzip2` as a library) and `file-roller` (an archive extractor) both required it, so all three would need to be removed together. This is exactly the kind of dependency chasing that high-level tools like `apt-get` handle automatically.

## 2. `rpm` Demo (Red Hat–Based)

This demo uses the RPM low-level packaging tool on a CentOS system.

List all installed packages:

```bash
$ rpm -qa | less
```

Search for a specific package:

```bash
$ rpm -qa | grep bzip2
```

This can return several related packages — a library, the command itself, and a development package.

### Listing a Package's Files with Command Substitution

Using `$(...)` command substitution, the output of one command can be fed directly as arguments to another:

```bash
$ ls -l $(rpm -ql bzip2) | less
```

`rpm -ql bzip2` lists every file in the `bzip2` package; that list is substituted in as arguments to `ls -l`, showing details for each installed file.

> [!NOTE]
> Among the listed files, `bunzip2` turns out to be a symbolic link to `bzip2`. The program checks the name it was invoked as (its "argument zero") to decide its behavior: called as `bunzip2`, it decompresses; called as `bzip2`, it compresses.

### Removing a Package (with a Dry Run First)

```bash
$ sudo rpm -e --test bzip2
```

The `--test` flag previews the result without actually removing anything — useful before committing to a potentially disruptive change. In this case, the test reveals that other packages (a library, `rpm-build`, and `perf`) depend on `bzip2`, so removing it would require removing those as well.

To check dependencies directly, without attempting a removal:

```bash
$ rpm -q --whatrequires bzip2
```

> [!NOTE]
> Higher-level tools (covered next) resolve dependencies like these automatically, whether installing or removing packages. `rpm` on its own is best suited to installing a package or two obtained directly — from a colleague, or off the network — rather than day-to-day package management.
