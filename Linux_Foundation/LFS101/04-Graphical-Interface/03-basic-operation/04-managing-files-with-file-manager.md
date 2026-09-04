# Managing Files with the File Manager

## 1. The File Manager by Desktop Environment

Every major Linux desktop environment includes a graphical file manager — the equivalent of File Explorer on Windows or Finder on macOS.

| Desktop Environment | File Manager |
| :--- | :--- |
| **GNOME** | **Files** (technically known as Nautilus) — the tool you'll use most often for everyday file management |
| **KDE Plasma** | **Dolphin** |
| **Cinnamon** | **Nemo** |

All three follow the same general principles covered here, with minor differences in layout and available options.

## 2. Opening the File Manager

| Method | Detail |
| :--- | :--- |
| Dock / sidebar icon | Typically resembles a file cabinet, labeled **Files** |
| Search | Type "Files" in the Activities Overview (GNOME) or your distribution's application launcher |
| Command line | `nautilus` (on GNOME-based systems) |

When it opens, it defaults to displaying your **Home** directory — the personal folder assigned to your user account, where all your personal files and directories are stored.

## 3. Understanding the Home Directory

Every user account has a dedicated home directory, typically located at `/home/username` (for example, `/home/student`). This is your personal space on the system: files you create and save are stored here by default, and no other standard user account can access it without permission.

When an account is created — during installation, or when a new user is added later — a standard set of subdirectories is automatically created within the home directory. These will be familiar from other operating systems:

| Folder | Purpose |
| :--- | :--- |
| **Documents** | Personal files and documents |
| **Downloads** | Default destination for files downloaded from the internet |
| **Desktop** | Files placed here appear on the desktop |
| **Pictures**, **Music**, **Videos** | Organized media folders |

The left panel of the file manager provides quick access to these common locations, as well as other areas of the system, such as connected drives and network locations.

## 4. Common Operations (Supplementary)

| Action | How |
| :--- | :--- |
| Copy / Cut / Paste | `Ctrl+C` / `Ctrl+X` / `Ctrl+V`, or drag-and-drop |
| Rename | Select the item and press `F2` |
| Select multiple items | `Ctrl+click` for individual items, `Shift+click` for a range, `Ctrl+A` for all |
| Create a new folder or file | Right-click empty space → **New Folder** / **New Document** |
| View properties | Right-click → **Properties** (size, type, permissions, timestamps) |

> [!NOTE]
> Most file managers also offer both a **list view** (detailed columns) and a **grid/icon view**, toggled from the toolbar or with `Ctrl+1` / `Ctrl+2` in GNOME Files.
