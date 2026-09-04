# Setting Default Applications

## 1. What Default Applications Are

When multiple applications can handle the same type of file or task — two browsers, two media players installed side by side — Linux lets you specify which one should be used by default.

## 2. Setting Defaults by Desktop Environment

| Desktop Environment | Where to Set Defaults |
| :--- | :--- |
| **GNOME** (Fedora and most others) | Settings → **Default Applications** |
| **GNOME** (Ubuntu) | Settings → **Apps → Default Apps** |
| **KDE Plasma** | System Settings → **Applications → Default Applications** — a similar set of options, with slightly more granular control |
| **Cinnamon** | System Settings → **Preferred Applications** |

From these panels, you can assign a preferred default for categories such as web browser, email client, calendar, music player, and video player.

> [!NOTE]
> The available options reflect only what's currently installed on the system, so the list varies from one machine to another.

This is directly comparable to **Default Apps** in Windows Settings, or the **General** tab within each application's own preferences on macOS.

> [!TIP]
> **Practical tip:** Default application settings become particularly relevant once you start installing additional software. If you install a second browser, for example, your system needs to know which one to open when you click a web link in an email. Setting your defaults early saves the confusion of applications opening in unexpected programs.

## 3. Per-File-Type Overrides From the File Manager (Supplementary)

The Settings panels above cover broad categories, but not every file type. For something more specific — a particular text editor for `.txt` files, or a particular image viewer for `.png` files — the file manager handles it directly:

1. Right-click the file and choose **Open With**.
2. Select the desired application (or **Other Application** to browse for one not listed).
3. Check **Set as default** so future files of that type open the same way automatically.
