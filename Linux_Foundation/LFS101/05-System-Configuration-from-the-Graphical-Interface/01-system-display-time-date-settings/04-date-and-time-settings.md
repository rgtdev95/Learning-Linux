How Linux Handles Time

Linux uses Coordinated Universal Time (UTC) internally for all timekeeping. UTC is the global standard for precise timekeeping and the basis for all time zones; it is similar to Greenwich Mean Time (GMT) but more precisely defined. Storing time internally as UTC is a deliberate design choice that ensures consistency across time zones, avoids complications with daylight saving time transitions, and keeps system logs accurate regardless of the machine's location.

The time displayed on your desktop is not stored as local time; it is derived from UTC and adjusted by your configured time zone. This means that changing your time zone does not alter the underlying system clock; it simply changes how the time is presented to you.

This distinction matters more than it might seem at first. If you dual-boot Linux and Windows on the same machine, you may notice a time discrepancy between the two operating systems after switching between them. This happens because Windows, by default, stores the hardware clock as local time rather than UTC. The two systems then interpret the same clock value differently. The cleanest fix is to configure Windows to use UTC as well, which can be done via a registry setting, though that is beyond the scope of this course.

Accessing Date and Time Settings

The full date and time configuration is found at Settings → Date & Time on most current distributions, including Ubuntu 24.04 and Fedora. On some distributions, including certain versions of openSUSE and older GNOME-based systems, this may be located under Settings → System → Date & Time instead. If you do not find it at the top level of Settings, check for a System subcategory in the sidebar.

From the Date & Time panel, you can:

•
Set the time zone
Select your region and city from a searchable list, or click your location on an interactive world map if your GNOME version supports it. The system clock updates immediately when the time zone is changed.

•
Toggle automatic date and time
When enabled, the system synchronizes with an internet time server automatically. This is the recommended setting for all users with an active network connection.

•
Toggle automatic time zone
Available on some distributions, this uses your network location to set the time zone automatically. Useful on laptops that travel between time zones.

•
Set the time format
Switch between 24-hour and 12-hour (AM/PM) display according to your preference.

For a quick adjustment to how the date and time appear on the top bar without opening the full Settings application, you can click directly on the clock in the top bar. Depending on your distribution and GNOME version, this may open a calendar popover that also provides access to notifications and, on some systems, a shortcut into the full Date & Time settings.

On some distributions, modifying the time zone or disabling automatic time synchronization requires administrator privileges. You may be prompted for your password before changes can be applied.

Date and Time Settings

Network Time Protocol

When Automatic Date & Time is enabled, Linux uses the Network Time Protocol (NTP) to keep the system clock accurate. NTP works by querying a network of highly precise reference servers distributed across the internet, including servers synchronized to atomic clocks, and making small, continuous adjustments to the local clock to keep it accurate.

In practice, this happens silently in the background and requires no user intervention. All major Linux distributions ship with NTP configured and running by default, referencing time servers operated or recommended by the distribution itself. On most current distributions, the NTP client is handled by systemd-timesyncd, a lightweight time synchronization service that is part of systemd. More advanced setups, such as servers that need highly precise timekeeping or that serve time to other machines on a local network, use a full NTP daemon such as chrony or ntpd, but for desktop use, systemd-timesyncd is sufficient and requires no configuration.

Enabling automatic time synchronization in the Date & Time settings  ensures that systemd-timesyncd is active. Disabling it stops the service and allows you to set the clock manually; this is useful in isolated environments without internet access, but not recommended for general use, as clocks that are not synchronized will drift gradually over time.

This is the direct equivalent of Set time automatically in Windows Settings or Set date and time automatically in macOS System Settings: the same concept, implemented at the operating system level.