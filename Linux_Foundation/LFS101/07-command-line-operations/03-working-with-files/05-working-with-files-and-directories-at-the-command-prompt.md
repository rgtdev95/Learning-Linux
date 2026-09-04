# Working with Files and Directories at the Command Prompt (Demo Notes)

This demo (CentOS 8 Stream) covers day-to-day file operations. The commands behave identically on any Linux distribution.

## 1. Creating Files

Two ways to create an empty (or small) file:

```bash
$ echo > file1
$ touch file2
```

`ls -l file1 file2` shows both were created at the same time.

## 2. Renaming and Removing Files

Rename with `mv`:

```bash
$ mv file1 file1-newname
```

Remove with `rm`:

```bash
$ rm file2
```

> [!TIP]
> It's a good idea to always use `-i` (interactive) when removing files:
> ```bash
> $ rm -i file1-newname
> ```
> This asks for confirmation before deleting. Many distributions set `-i` as the default for `rm`, giving a chance to change your mind before anything is removed.

## 3. Creating Directories

`mkdir` can create more than one directory in a single command:

```bash
$ mkdir dir1
$ mkdir dir2 dir3
```

Adding files inside a directory works the same way as anywhere else:

```bash
$ touch dir2/file1
$ touch dir2/file2
```

`ls -lR` recursively lists everything: `dir1` and `dir3` are empty, `dir2` contains the two new files.

## 4. Removing Directories

`rmdir` only removes **empty** directories:

```bash
$ rmdir dir*
```

This removes `dir1` and `dir3`, but fails on `dir2` because it still contains files.

To remove a directory and everything inside it, use `rm -rf` instead:

```bash
$ rm -rf dir2
```

> [!WARNING]
> Be very careful with `rm -rf`. Given the wrong argument, it can wipe out far more than intended — even an entire system. It's the standard way to remove a whole directory tree, but it deserves caution every time.
