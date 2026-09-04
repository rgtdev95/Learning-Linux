# Manual Sections

The man pages are organized into numbered sections, 1 through 9. These are occasionally called "chapters" — the two terms mean the same thing, though "section" is the standard. In some cases, a letter is appended to the section number to mark a specific topic area; for example, many pages describing part of the X Window API live in section 3X.

## 1. Specifying a Section

The section number lets you tell `man` exactly which page you want. This matters because it's common for several pages in different sections to share the same name, especially for library functions and system calls that happen to be named the same as a command — for instance, there's both a command and a system call documented under the name `socket`.

To specify a section, put its number before the topic name:

```bash
$ man 2 socket
```

To display every page matching a given name, one after another across all sections, use `-a`:

```bash
$ man -a socket
```

## 2. Sections at a Glance

| Section | Contents | Examples |
| :--- | :--- | :--- |
| 1 | Executable programs and shell commands | `ls`, `cp`, `grep` |
| 2 | System calls (functions provided by the kernel) | `open()`, `read()`, `write()` |
| 3 | Library calls (functions in program libraries) | `printf()`, `malloc()` |
| 4 | Special files | Device files found in `/dev`, such as `/dev/null` |
| 5 | File formats and conventions | Configuration files like `/etc/fstab`, file formats like `crontab(5)` |
| 6 | Games | Games and screensavers |
| 7 | Miscellaneous | Conventions, macro packages, standards |
| 8 | System administration commands | Privileged commands used by root, such as `fdisk` and `mount` |
| 9 | Kernel routines | Non-standard internal kernel interfaces |

> [!NOTE]
> Section 9 is inconsistently populated across distributions — many systems have few or no section 9 pages.
