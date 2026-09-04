# Exploring the Filesystem

## 1. Getting a Bird's-Eye View: `tree`

Navigating up and down the filesystem tree one directory at a time can get tedious. The `tree` command gives a bird's-eye view of the filesystem tree; `tree -d` shows just the directories, suppressing file names.

> [!NOTE]
> `tree` is not installed by default on Ubuntu. If the command isn't found, install it with `sudo apt install tree`.

## 2. Useful Commands

| Command | Result |
| :--- | :--- |
| `cd /` | Changes to the root (`/`) directory, or any path supplied |
| `ls` | Lists the contents of the present working directory |
| `ls -a` | Lists all files, including hidden files and directories (names starting with `.`) |
| `tree` | Displays a tree view of the filesystem |

## 3. Demo Walkthrough

1. **Absolute path** — from `/usr`, run `cd /usr/local/live` to reach it directly.
2. Return with `cd /usr`.
3. **Relative path** — from `/usr`, run `cd local/live` to reach the same `/usr/local/live` directory.
4. **Root directory** — `cd /` moves to the root of the filesystem.
5. **Listing contents** — `ls` lists the files and directories in the current location; `ls -a` also includes hidden ones.
6. **Tree view** — `tree` shows a full tree view of the filesystem from the current location; `tree -d` restricts it to directories only.
