# Hard and Soft Links

## 1. Hard Links

The `ln` utility creates hard links. Unlike a standard copy, a hard link acts as an additional name for the exact same data on disk.

Assuming `file1` already exists, a hard link named `file2` is created with:

```bash
$ ln file1 file2
```

While it appears as if two files exist, they share the same **inode number** — the unique identifier for the underlying data on disk. This can be verified with `ls -li`:

```bash
$ ls -li file1 file2
```

In the output, the first column shows the identical inode number for both names, and the second column (the link count) increments to `2`.

### Data Preservation

Because both filenames point to the same data, removing one name does not delete the file — the data remains accessible via the remaining name. The file is only actually deleted from disk once *all* hard links to it have been removed.

### Use Caution with Editors

> [!WARNING]
> Avoid using hard links for files you intend to edit. Many modern editors perform "atomic saves" — writing changes to a new file and renaming it over the original. This breaks the hard link: the edited name now points to new, separate data, while the other name still refers to the original inode and its old contents. The two names are no longer the same file.

This behavior varies by editor — some, such as `vi` and `gedit`, edit the file in place and keep the hard link intact, so whether the link survives depends on the tool used.

## 2. Soft (Symbolic) Links

Soft links, often called **symlinks**, are created with the `-s` option:

```bash
$ ln -s file1 file3
```

Inspecting a symbolic link with `ls -li` shows it has its own unique inode number and a distinct file type indicator — an `l` at the start of the permissions string, along with a `->` pointing to the target. Unlike a hard link, a symbolic link does not share the original file's data; it acts as a "pointer," or shortcut, to the original file path.

### Key Characteristics

| Characteristic | Detail |
| :--- | :--- |
| **Cross-filesystem support** | Symlinks can point to objects across different partitions, disks, or external media; a hard link is confined to a single filesystem |
| **Minimal overhead** | Symlinks occupy very little space — they store the text path to the target rather than a copy of the data itself |
| **Flexibility** | A symlink can be updated to point to a new location without affecting the source file, making it a convenient way to create a short, stable name for a long or frequently changing path |

> [!WARNING]
> **Watch for dangling links.** Because a symlink refers to a path rather than to the data directly, it can point to a target that no longer exists or isn't currently available. If the target is deleted, moved, or not yet mounted, the result is a "dangling link" pointing to an invalid object.
