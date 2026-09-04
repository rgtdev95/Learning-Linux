# System Settings

## 1. Accessing System Settings

The **Settings** application is the central location for configuring your system. From here, you can adjust display settings, manage network connections, change the date and time, configure users, and much more — all without touching the command line.

| Method | Detail |
| :--- | :--- |
| System menu | Click the icon cluster in the upper-right corner → select the **Settings** icon (typically a gear) |
| Search | Type "Settings" in the Activities Overview |
| Dock (Ubuntu) | Settings is pinned to the sidebar dock by default |

> [!NOTE]
> The layout of the Settings application varies somewhat between distributions and GNOME versions, so the exact location of a particular option may differ from what's shown in this course. If a setting can't be found immediately, scanning the sidebar usually turns it up — most things are where you'd intuitively expect them to be.

## 2. Navigating System Settings

The sidebar organizes configuration options into logical categories. Selecting a category opens its options in the main panel. Commonly used sections include:

| Section | Covers |
| :--- | :--- |
| **Displays** | Screen resolution, refresh rate, multi-monitor configuration |
| **Network** / **Wi-Fi** | Wired and wireless connection management |
| **Date & Time** | Time zone and automatic time synchronization |
| **Users** | User accounts, passwords, login pictures |
| **Apps** / **Default Applications** | Which application handles each file type or task |

> [!NOTE]
> On some distributions, certain options are nested one level deeper — on older Ubuntu versions, for example, display settings are found under **Devices → Displays** rather than directly under **Displays**. If an option doesn't appear where expected, check for a sub-category.

For example, the **Users** panel (which may sit under a **System** sub-category) is where login pictures, passwords, and other per-account attributes are configured.

## 3. GNOME Tweaks and Extensions

As covered in [Changing the Desktop Theme](../../04-graphical-interface/01-graphical-desktop/04-graphical-desktop-background-and-themes.md), **GNOME Tweaks** and **GNOME Extensions** are the tools to reach for when the standard Settings application doesn't expose what's needed. Several settings users would reasonably expect to find in Settings — controlling which applications launch at login, fine-tuning font rendering, adjusting keyboard behavior — are only accessible through these tools.

### Startup Applications

To launch a specific application automatically at every login, configure it in **GNOME Tweaks → Startup Applications**. Some modern applications include their own "Start at Login" toggle in their preferences, but GNOME Tweaks remains the only reliable graphical method for managing startup behavior across all distributions.

### Keyboard Layout and Behavior

The division of keyboard settings between the two tools has shifted in recent GNOME versions:

| Setting | Where |
| :--- | :--- |
| Basic language layouts, key repeat | **Settings → Keyboard** (current distributions such as Ubuntu 24.04, Fedora 40+) |
| Advanced remapping (e.g., CapsLock as an additional Ctrl or Escape key) | **GNOME Tweaks → Keyboard & Mouse → Additional Layout Options** |

### Managing Extensions

On current distributions running GNOME 46+ (Ubuntu 24.04, Fedora 40+, RHEL 10, openSUSE Tumbleweed), extension management has been fully removed from GNOME Tweaks and lives entirely in the dedicated **Extensions** app. On Fedora and openSUSE, a popular third-party alternative called **Extension Manager** is widely used — unlike the default Extensions app, it allows browsing and installing extensions directly, without needing a browser connector to the GNOME Extensions website.

> [!WARNING]
> Major GNOME version jumps frequently break existing extensions. On a cutting-edge distribution such as Fedora 43/44 or openSUSE Tumbleweed (potentially GNOME 49/50), always check extension compatibility in Extension Manager before updating, or after a major distribution upgrade.

### Launching GNOME Tweaks Without a Menu Entry

On some distributions — particularly RHEL or minimal Fedora installations — GNOME Tweaks may not appear in the application grid immediately after installation. Press **Alt+F2**, type `gnome-tweaks`, and press Enter. This opens a run dialog that accepts any valid application name, a useful shortcut whenever a newly installed application doesn't appear in the menu right away.
