# The man Pages

## 1. What man Pages Are

The man pages are the most widely used source of Linux documentation. They provide in-depth reference material on programs and utilities, as well as configuration files and programming interfaces (such as system calls, library routines, and the kernel). They are present on every Linux distribution and are always right at your fingertips in the terminal.

> [!NOTE]
> If you've used Windows or a Mac, think of `man` as the equivalent of pressing F1 or opening an application's Help menu — except instead of a different help system for every program, `man` gives you one consistent command that documents virtually everything on the system. macOS users already have this: because macOS is UNIX-based, the Terminal app on any Mac responds to `man ls` exactly as on Linux.

To look something up, type `man` followed by the name of the topic:

```bash
$ man ls
```

> [!NOTE]
> The man page system dates back to the earliest versions of UNIX in the early 1970s — the name `man` is simply short for "manual." Man pages are often converted into other formats, such as PDFs and web pages, and many are also browsable online.

## 2. Navigating a man Page

The `man` program searches, formats, and displays manual entries. Because many topics carry a lot of detail, the output is piped through a pager program (usually `less`), so you can read it one screen at a time, nicely formatted for the terminal.

| Action | Key |
| :--- | :--- |
| Scroll | Up/Down arrow keys or Spacebar |
| Search | `/` followed by the search keyword, then Enter (`n` jumps to the next match) |
| Quit | `q` |

> [!TIP]
> Because `less` is used throughout Linux (for viewing logs, file outputs, and documentation), these navigation keys are worth memorizing early.

## 3. Searching for Commands

A single topic may have more than one page associated with it, and there's a default order that determines which one you see when nothing further is specified. Two search helpers are built in:

| Option | Effect |
| :--- | :--- |
| `man -f <topic>` | Lists available pages that match a name exactly — identical to the `whatis` command |
| `man -k <keyword>` | Searches page descriptions for a keyword, finding related pages even when the word isn't in the command name — identical to the `apropos` command |

> [!TIP]
> `-k` is especially handy when the exact command name isn't known — much like typing a topic into the search box of a Windows or Mac help system and letting it surface related entries. For example, `man -k compress` displays the various compression tools installed on the system.

The default search order is defined in a configuration file: `/etc/manpath.config` on Ubuntu and Debian systems, or `/etc/man_db.conf` on some other distributions such as Fedora, RHEL, and openSUSE. The order runs roughly, but not exactly, in ascending numerical order by section.

## 4. Demo Walkthrough

This demo looks up information about sockets:

1. `man socket` — opens section 2 (the Linux Programmer's Manual) by default, a general page covering sockets and the protocols they can use.
2. `man -f socket` — lists every page named `socket` across all sections (five, in this case). Identical to `whatis socket`.
3. `man 7 socket` — jumps straight to the more detailed section 7 page.
4. `man -a socket` — pages through every matching entry, one after another. Space pages through the current entry; `q` moves to the next match, or `Ctrl+C` exits out of the whole sequence early.
5. `man -k socket` — lists every page whose description mentions "socket" — a long list, since sockets touch many parts of the system. Identical to `apropos socket`.
