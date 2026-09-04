# Locating and Running Applications Using the File Manager, and Working with Text Files

## Demo Walkthrough (Fedora / GNOME)

This demo combines locating and launching applications, browsing the filesystem, and creating and editing a text file.

### 1. Launching Firefox

- **Applications** menu (upper-left) → **Favorites** → Firefox, or scroll down to the **Internet** category → Firefox.
- Alternative: click **Activities** (upper-left) — Favorites are also listed at the bottom of the overview.
- Closing an application: click the **X** in the corner of its window.

### 2. Opening the File Manager

- From the Favorites bar: click the icon that looks like a **file cabinet**.
- Or: **Applications** → **Files**.
- Files opens showing the system, starting at the **Home** directory.

### 3. Switching Views

- Files defaults to **Icon view**.
- Switching to **List view** shows when files were created and, depending on configuration, who owns them.

### 4. Showing Hidden Files

- Click the **Settings** menu in the upper-right corner of the Files window.
- Select **Show Hidden Files** to reveal dotfiles such as `.bashrc`.

### 5. Creating and Saving a New File

1. **Applications** → **Accessories** → **Text Editor** — this is `gedit`, renamed "Text Editor" in recent GNOME versions.
2. Type some content into the new, unnamed document.
3. Click **Save As** (required, since the file doesn't have a name yet).
4. Accept the suggested filename — Text Editor proposes one based on the content typed.
5. Close the editor; the new file now appears in the Files window.

### 6. Deleting the File

1. Right-click the file → **Move to Trash**.
2. Open **Trash** from the left panel.
3. Right-click the file within Trash → **Delete from Trash** to remove it permanently.

> [!NOTE]
> Some distributions show a **Delete Permanently** option directly on the file, skipping the Trash. On this Fedora system, that option wasn't available — permanent deletion required going through Trash first.

## Key Takeaway

This walkthrough ties together earlier lessons in one flow: [Launching Applications](01-launching-applications.md), [Viewing Files and Directories](05-viewing-files-and-directories.md), [Editing a File](07-editing-a-file.md), and [Deleting Files and Using the Trash](08-deleting-files-and-using-the-trash.md) — locating and running an app, browsing and revealing hidden files, and creating, saving, and cleaning up a text file, all from the graphical desktop.
