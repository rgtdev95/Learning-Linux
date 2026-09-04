# Moving, Renaming, and Removing Files

## 1. `mv`: Move and Rename

`mv` (short for "move") is used to move and rename files. It does double duty:

- Simply rename a file
- Move a file to another location, possibly changing its name at the same time

Both actions use the same syntax:

```bash
$ mv source destination
```

Whether the file is renamed or moved depends on what's given as the destination.

```bash
$ mv notes.txt notes_old.txt
```

This renames `notes.txt` to `notes_old.txt` in the current directory.

```bash
$ mv notes.txt /home/student/documents/
```

This moves `notes.txt` into the `documents` directory, keeping its name. A new name can be given at the end of the path to move and rename in one step.

> [!WARNING]
> The destination directory must already exist. If it doesn't, the result depends on the trailing slash: written with a trailing `/` as above, `mv` reports an error; written without one (`mv notes.txt /home/student/documents`), `mv` instead renames `notes.txt` to a file called `documents` — rarely what was intended.

## 2. `rm`: Remove

`rm` (short for "remove") deletes files:

```bash
$ rm notes.txt
```

By default, `rm` only removes files, not directories — running it on a directory fails with "Is a directory." To remove a directory and its contents, add the recursive flag (`rm -r`, or `rm -rf` to also suppress prompts).

> [!WARNING]
> If you're not certain about removing files that match a pattern, it's always good to run `rm` interactively (`rm -i`), which prompts for confirmation with `y` or `n` before every removal. `rm -f` does the opposite — it forcefully removes files without any prompts or warnings, so use it with care.

| Command | Usage |
| :--- | :--- |
| `mv` | Rename or move a file |
| `rm` | Remove a file |
| `rm -f` | Forcefully remove a file (no prompts) |
| `rm -i` | Interactively remove a file (prompts before each) |
