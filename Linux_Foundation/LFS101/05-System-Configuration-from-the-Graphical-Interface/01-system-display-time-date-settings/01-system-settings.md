Accessing System Settings

The Settings application is the central location for configuring your system. From here, you can adjust display settings, manage network connections, change the date and time, configure users, and much more, all without touching the command line.

On GNOME-based distributions, the quickest way to open Settings is to click the icon cluster in the upper-right corner of the screen and select the Settings icon, typically represented by a gear. You can also search for "Settings" in the Activities Overview. On Ubuntu specifically, Settings is also pinned to the sidebar dock by default.

The layout of the Settings application varies somewhat between distributions and GNOME versions, so the exact location of a particular option may differ from what is shown in this course.



System Settings Panel
(Select the image to see an enlarged version)

If you cannot find a setting immediately, it is worth scanning through the sidebar; most things are where you would intuitively expect them to be.

Navigating System Settings

The Settings sidebar organizes configuration options into logical categories. Selecting any category opens its options in the main panel. Some commonly used sections include:

•
Displays - screen resolution, refresh rate, and multi-monitor configuration.

•
Network or Wi-Fi - wired and wireless connection management.

•
Date & Time - time zone and automatic time synchronization.

•
Users - user accounts, passwords, and login pictures.

•
Apps or Default Applications - which application handles each file type or task.

On some distributions, certain options are nested one level deeper. On older Ubuntu versions, for example, display settings are found under Devices → Displays rather than directly under Displays. If an option does not appear where you expect it, check for a sub-category.


Configuring Applications on Ubuntu

For example, you can select the Users icon (which may be under System) to set values for system users, such as their login picture, password, etc.


Configuring the User Attributes

GNOME Tweaks and Extensions

As covered in Chapter 4, GNOME Tweaks and GNOME Extensions are the tools to reach for when the standard Settings application does not expose what you need. This is worth revisiting here in the context of system configuration, because several settings that users would reasonably expect to find in Settings (such as controlling which applications launch at login, fine-tuning font rendering, or adjusting keyboard behavior) are only accessible through these tools.

Select the plus (+) sign next to the option name to view a few things worth knowing as you work through the configuration tasks in this chapter.


Startup applications
If you want a specific application to launch automatically every time you log in, this is configured in GNOME Tweaks under the Startup Applications tab. While some modern applications include a "Start at Login" toggle in their own preferences, GNOME Tweaks remains the only reliable graphical method for managing startup behavior across all distributions.


Keyboard layout and behavior
The division of keyboard settings between the two tools has shifted in recent GNOME versions. Basic language layouts and key repeat settings are now handled in Settings → Keyboard on current distributions such as Ubuntu 24.04 and Fedora 40 and later. Advanced remapping options, such as making the CapsLock key behave as an additional Ctrl or Escape key, remain in GNOME Tweaks → Keyboard & Mouse under Additional Layout Options.


Managing extensions
On current distributions running GNOME 46 and later (including Ubuntu 24.04, Fedora 40+, RHEL 10, and openSUSE Tumbleweed), extension management has been fully removed from GNOME Tweaks and lives entirely in the dedicated Extensions app. On Fedora and openSUSE, a popular third-party alternative called Extension Manager is widely used; unlike the default Extensions app, it allows you to browse and install extensions directly without requiring a browser connector to the GNOME Extensions website.

Compatibility note:
If you are running a cutting-edge distribution such as Fedora 43/44 or openSUSE Tumbleweed, you may be on GNOME 49 or 50. Major GNOME version jumps frequently break existing extensions. Always check extension compatibility in the Extension Manager before updating or after a major distribution upgrade.


Launching GNOME Tweaks without a menu entry
On some distributions, particularly RHEL or minimal Fedora installations, GNOME Tweaks may not appear in the application grid immediately after installation. In that case, press Alt+F2, type ‘gnome-tweaks’, and press Enter. This key combination opens a run dialog that accepts any valid application name, a useful shortcut whenever a newly installed application does not appear in the menu immediately.