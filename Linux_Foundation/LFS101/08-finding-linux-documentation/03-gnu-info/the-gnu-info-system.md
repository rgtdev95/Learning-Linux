# The GNU Info System

The next source of Linux documentation is the **GNU Info** system — the GNU Project's preferred documentation format, designed as a richer alternative to man pages.

Where a man page is essentially one long scrollable document, an Info manual is structured like a mini-website or e-book: broken into linked pages navigated between using menus and cross-references. (This hyperlinked design actually predates the World Wide Web.) Info documentation can be read directly from the command line, through a GUI browser, in print, or online.

> [!NOTE]
> The Info interface can feel dated compared to modern web browsers, and uses different shortcuts than `man`. It's often the most complete source of documentation available for GNU utilities. For a quick comparison, try running `man ls` and then `info ls` to see how much extra depth the Info version provides.

## 1. Using info from the Command Line

To open the top-level directory of all available topics, run `info` with no arguments:

```bash
$ info
```

To jump directly to a specific utility:

```bash
$ info ls
```

`info` searches all installed Info files for that topic.

## 2. How an Info Page Is Structured

Each page in Info is called a **node**. Nodes act as the chapters and sections of a manual, arranged in a tree structure: a top-level node branches into chapters, which branch into sub-sections.

To jump between nodes, links called **items** are used:

- **Menu items** are marked with an asterisk (`*`) at the start of a line.
- **Cross-references** end with a double colon (`::`).

## 3. Navigation Keys

| Key | Function |
| :--- | :--- |
| `Tab` | Move cursor to the next link (`*` or `::`) |
| `Enter` | Follow the link currently under the cursor |
| `n` | Move to the **n**ext node (at the same level) |
| `p` | Move to the **p**revious node (at the same level) |
| `u` | Move **u**p to the parent node |
| `l` | Go back to the **l**ast node visited (like a browser's Back button) |
| `h` | Open Info's built-in interactive tutorial |
| `q` | Quit and return to the shell prompt |

> [!TIP]
> Info's navigation keys are case-sensitive and differ from the `less` pager used by `man`. If you ever get lost, press `l` (lowercase L) to retrace your steps, `h` for help, or `q` to exit.

## 4. Demo Walkthrough

This demo explores the `make` utility's Info documentation:

1. `info make` — opens the top of the Info page (the head node).
2. `/Example` then Enter — searches for "Example," landing on the "Rule Example" node.
3. `n` — advances to the next node at the same level ("Rule Syntax," then "Prerequisite Types").
4. `p` — moves back to the previous node.
5. `/` then Enter — repeats the last search, jumping to a later match ("wildcard examples").
6. `u` — moves up a level at a time: from a subsection, to the enclosing chapter, to the very top.
7. `h` — shows all available keystrokes and what they do, with focus shifting to the help window.
8. `q` — exits Info back to the shell prompt.
