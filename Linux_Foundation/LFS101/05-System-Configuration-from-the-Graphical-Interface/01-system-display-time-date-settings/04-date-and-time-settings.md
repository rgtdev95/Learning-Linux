# Date and Time Settings

## 1. How Linux Handles Time

Linux uses **Coordinated Universal Time (UTC)** internally for all timekeeping. UTC is the global standard for precise timekeeping and the basis for all time zones — similar to Greenwich Mean Time (GMT), but more precisely defined.

Storing time internally as UTC is a deliberate design choice: it ensures consistency across time zones, avoids complications with daylight saving time transitions, and keeps system logs accurate regardless of the machine's location.

> [!NOTE]
> The time displayed on the desktop is not stored as local time — it's derived from UTC and adjusted by the configured time zone. Changing the time zone doesn't alter the underlying system clock; it only changes how the time is presented.

### Dual-Boot Time Discrepancies

If Linux and Windows are dual-booted on the same machine, a time discrepancy can appear between the two after switching between them. This happens because Windows, by default, stores the hardware clock as **local time** rather than UTC — the two systems then interpret the same clock value differently.

> [!TIP]
> The cleanest fix is configuring Windows to use UTC as well, via a registry setting — beyond the scope of this course, but worth knowing the cause if the clock looks wrong after switching operating systems.

## 2. Accessing Date and Time Settings

The full configuration is found at **Settings → Date & Time** on most current distributions, including Ubuntu 24.04 and Fedora. On some distributions — certain versions of openSUSE and older GNOME-based systems — this may instead be located under **Settings → System → Date & Time**. If it isn't at the top level, check for a **System** sub-category in the sidebar.

From the Date & Time panel:

| Option | Detail |
| :--- | :--- |
| **Set the time zone** | Select a region and city from a searchable list, or click a location on an interactive world map if supported. The system clock updates immediately. |
| **Toggle automatic date and time** | Synchronizes with an internet time server automatically — recommended for anyone with an active network connection. |
| **Toggle automatic time zone** | Available on some distributions; uses network location to set the time zone automatically. Useful on laptops that travel between time zones. |
| **Set the time format** | Switch between 24-hour and 12-hour (AM/PM) display. |

> [!TIP]
> For a quick adjustment without opening the full Settings application, click directly on the clock in the top bar. Depending on the distribution and GNOME version, this opens a calendar popover that also provides access to notifications and, on some systems, a shortcut into the full Date & Time settings.

> [!NOTE]
> On some distributions, modifying the time zone or disabling automatic time synchronization requires administrator privileges — expect a password prompt before the change is applied.

## 3. Network Time Protocol (NTP)

When **Automatic Date & Time** is enabled, Linux uses the **Network Time Protocol (NTP)** to keep the system clock accurate. NTP works by querying a network of highly precise reference servers distributed across the internet — including servers synchronized to atomic clocks — and making small, continuous adjustments to the local clock.

This happens silently in the background and requires no user intervention. All major Linux distributions ship with NTP configured and running by default, referencing time servers operated or recommended by the distribution itself.

| Use Case | Tool |
| :--- | :--- |
| Desktop use (sufficient, no configuration needed) | **systemd-timesyncd** — a lightweight time synchronization service that's part of systemd |
| Servers needing highly precise timekeeping, or serving time to other machines on a local network | A full NTP daemon such as **chrony** or **ntpd** |

Enabling automatic time synchronization in Date & Time settings ensures `systemd-timesyncd` is active. Disabling it stops the service and allows the clock to be set manually — useful in isolated environments without internet access, but not recommended for general use, since unsynchronized clocks gradually drift over time.

> [!NOTE]
> This is the direct equivalent of **Set time automatically** in Windows Settings, or **Set date and time automatically** in macOS System Settings — the same concept, implemented at the operating system level.
