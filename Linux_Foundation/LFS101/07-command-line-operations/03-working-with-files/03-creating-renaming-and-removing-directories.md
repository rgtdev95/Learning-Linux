# Creating, Renaming, and Removing Directories

## 1. `mkdir`: Create a Directory

```bash
$ mkdir sampdir
```

Creates a directory named `sampdir` under the current directory.

```bash
$ mkdir /usr/sampdir
```

Creates a directory called `sampdir` under `/usr`.

> [!NOTE]
> This requires write permission on `/usr`, so as a regular user it will typically fail with "Permission denied" unless `sudo` is used.

If a directory's parent directories don't exist yet, use `-p`:

```bash
$ mkdir -p projects/2026/reports
```

This creates `projects`, `projects/2026`, and `projects/2026/reports` all in one step; without `-p`, `mkdir` would fail if any parent in the path is missing.

## 2. Renaming a Directory

To rename a directory, use `mv`, exactly as with a file:

```bash
$ mv projects archive
```

## 3. Removing a Directory

There are two options, depending on whether the directory is empty.

### `rmdir`: Empty Directories Only

```bash
$ rmdir sampdir
```

The directory must be empty (including hidden files, not just visible ones) or the command fails.

### `rm -r`: Directory and Everything Inside It

```bash
$ rm -r sampdir
```

The `-r` flag makes the removal recursive — it drills down through all subdirectories, all the way down the tree. To also skip any prompts, add `-f`:

```bash
$ rm -rf sampdir
```

> [!WARNING]
> This deletes permanently, with no confirmation and no way to undo it. The `-r` flag makes the removal recursive (contents and subdirectories included), and `-f` forces it without prompting. While learning, consider `rm -ri sampdir` instead, which asks for confirmation before each deletion.

| Command | Usage |
| :--- | :--- |
| `mkdir` | Create a directory |
| `mkdir -p` | Create a directory along with any missing parent directories |
| `mv` | Rename or move a directory |
| `rmdir` | Remove an empty directory |
| `rm -r` | Recursively remove a directory and its contents |
| `rm -rf` | Recursively remove a directory, forcing without prompts |
