# Working with Files: Overview

To manage data well, it helps to know the basic file operations in Linux. The command line can be used to look at file contents, create or update files, rename folders, and remove files no longer needed — keeping files organized and correct.

This section covers the key Linux commands needed to create, view, move, and manage files and folders.

## Viewing Files

| Command | Usage |
| :--- | :--- |
| `cat` | Used for viewing shorter files; provides no scroll-back |
| `tac` | Views a file backwards, starting with the last line (`tac` is `cat` spelled backwards) |
| `less` | Used to view larger files; a paging program that pauses at each screen full of text, provides scroll-back, and lets you search and navigate within the file |
| `tail` | Prints the last 10 lines of a file by default; change the count with `-n 15` or `-15` for the last 15 lines |
| `head` | The opposite of `tail`; prints the first 10 lines of a file by default |

> [!NOTE]
> In `less`, use `/` to search forward for a pattern and `?` to search backward. An older program named `more` is still around, but has fewer capabilities — hence the joke, "`less` is `more`."

## Demo Walkthrough

This demo uses a file called `ready-for.sh` with 5,127 lines (confirmed with `wc`).

1. **`cat`** prints the whole file at once — fast, but scrolls past instantly for a file this size. `cat -n` adds line numbers as it goes.
2. **`less ready-for.sh`** pages through one screen at a time; pressing the space bar advances to the next screen. `less -N` also shows line numbers.
3. **`head ready-for.sh`** shows the first 10 lines by default; passing a number (`head -20 ready-for.sh`) shows the first 20 instead.
4. **`tail`** works the same way for the end of the file — `tail -20` shows the last 20 lines.
5. **`tac`** prints the entire file in reverse, line by line.

These are the day-to-day utilities for looking at the contents of text files.
