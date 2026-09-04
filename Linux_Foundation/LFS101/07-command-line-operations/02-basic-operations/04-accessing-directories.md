# Accessing Directories

## 1. The Default Directory

When you first log into a system or open a terminal, the default directory should be your home directory. Confirm the exact location with:

```bash
$ echo $HOME
```

`echo` prints a line of text, or the value of a variable, to the screen — used constantly in scripts and for inspecting environment variables.

> [!NOTE]
> Where a terminal actually lands can depend on how it was opened. Launching one from the Activities search, the dash, or a shortcut like `Ctrl+Alt+T` lands in the home directory, while right-clicking the desktop background and choosing **Open in Terminal** opens the session in that folder instead — usually `$HOME/Desktop`.

## 2. Basic Navigation Commands

| Command | Result |
| :--- | :--- |
| `pwd` | Displays the present working directory |
| `cd ~` or `cd` | Changes to the home directory (`~` is shorthand for home) |
| `cd ..` | Changes to the parent directory |
| `cd -` | Changes to the previous working directory |

## 3. Demo Walkthrough

1. Start in the home directory, move to `/tmp`, and confirm with `pwd`.
2. Return home three equivalent ways — a plain `cd`, `cd $HOME`, or `cd ~` — all land in the same place (e.g., `/home/student`).
3. For tracking more than one previous directory, `pushd`/`popd`/`dirs` manage a directory stack:
   - `pushd /tmp` — moves to `/tmp`, recording `~` on the stack.
   - `pushd /usr/share/doc` — moves there, adding another entry; the stack now holds `/usr/share/doc`, `/tmp`, and `~`.
   - `popd` — returns to `/tmp`.
   - `dirs` — lists everything currently on the stack, useful if you've lost track of where you've been.
   - `pushd` with no argument swaps the top two entries on the stack, letting you toggle back and forth between them.
   - A final `popd` returns to the home directory.

> [!NOTE]
> See [Navigating the Directory History](08-navigating-the-directory-history.md) for a full breakdown of how `pushd`, `popd`, and `dirs` work.
