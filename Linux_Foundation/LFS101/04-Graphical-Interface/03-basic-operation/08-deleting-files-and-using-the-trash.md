# Deleting Files and Using the Trash

## 1. How Deletion Works in Nautilus

Deleting files in Nautilus works similarly to other operating systems: deleted items are moved to the **Trash** rather than being permanently removed immediately, giving you the opportunity to recover them if needed.

## 2. Moving Files to the Trash

1. Select the item(s) to delete. Multiple items can be selected by holding **Ctrl** and clicking, or **Shift** and clicking to select a range.
2. Right-click and choose **Move to Trash**, or press **Ctrl+Delete**.

Deleted items are moved to the Trash folder, located at `.local/share/Trash/files/` within your home directory. To browse and restore items, click **Trash** in the left panel of the file manager.

## 3. Restoring a File (Supplementary)

Within the Trash folder, right-click a file and choose **Restore** to return it to its original location.

## 4. Permanently Deleting Files

| Action | Result |
| :--- | :--- |
| Right-click **Trash** → **Empty Trash** | Permanently removes everything currently in the Trash |
| Select a file → `Shift+Delete` | Bypasses the Trash entirely, deleting the file immediately |

> [!WARNING]
> Permanent deletion — whether by emptying the Trash or using `Shift+Delete` — cannot be undone. Use it with care.

## 5. Never Delete Your Home Directory

> [!WARNING]
> Never delete your Home directory. It contains not only your personal files, but also the configuration files for your desktop environment and applications, stored in hidden folders within it. Deleting it would almost certainly prevent you from logging in, and would result in the loss of all your personal settings and data.
