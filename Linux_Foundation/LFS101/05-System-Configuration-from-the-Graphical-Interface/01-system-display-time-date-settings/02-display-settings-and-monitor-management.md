Display Settings

Adjusting Your Display

To manage how your system presents information on screen, navigate to Settings → Displays. On some distributions and older GNOME versions, this may be found under Settings → Devices → Displays. You can also reach it by right-clicking anywhere on the desktop and selecting Display Settings.

Most current distributions, including Ubuntu 24.04 and Fedora, will automatically detect and select the Native resolution of your monitor, which produces the sharpest image. While you can override this, selecting a non-native resolution typically results in a blurry or stretched interface and is not recommended unless there is a specific reason to do so.

For users with displays that support higher refresh rates, the Refresh Rate dropdown lets you select a higher frequency (such as 120Hz or 144Hz) for a smoother, more fluid visual experience. This setting is particularly relevant for gaming or when working with animations and video.


Fractional Scaling
To enable fractional scaling on GNOME, open Settings → Displays and toggle on Fractional Scaling if it is not already active. The intermediate scale options will then appear in the scale selector.

Night Light

Configuring Multiple Monitors

When you connect an additional monitor, the system typically detects it and extends the desktop automatically. The Displays panel provides a visual map of all connected screens, which you can interact with directly:


Arrange monitors by dragging the screen icons to match their physical positions on your desk. This ensures the mouse cursor moves logically from one screen to the next.


Designate a Primary Display - this is the monitor that will show the top bar, including the Activities button and system clock. Dock behavior on secondary displays may vary depending on your distribution settings; on Ubuntu, you can configure the dock to appear on all displays or only the primary one in Settings → Ubuntu Desktop.

•
Select a display mode: Join Displays - It extends the desktop across all monitors into a single continuous workspace. This is the standard working configuration.

•
Mirror - shows identical content on all connected displays. This is the typical choice for presentations.

•
Single Display - disables all but the selected monitor.

When you apply a new display configuration, a confirmation dialog will appear with a 15-second countdown. If you do not select Keep Changes within that time, the system automatically reverts to the previous working configuration.

This safety mechanism prevents you from being left with an unusable or blank display if a setting does not work as expected.



Multiple Displays
(Select the image to see an enlarged version)

A Note on the Underlying Display Infrastructure

While these settings are straightforward to use, it is worth briefly understanding what is happening beneath the surface. As discussed in Chapter 4, Linux uses a display server to draw windows and manage input from the keyboard and mouse. Current distributions, Ubuntu 22.04 and later, Fedora, and RHEL, use Wayland as the default display server, which handles modern features like fractional scaling and multi-monitor configuration more reliably than its predecessor.

The legacy X11 session remains available on Ubuntu 24.04 and some other current distributions, primarily for compatibility with older hardware or specific enterprise environments that require it. However, it is being phased out; Ubuntu 25.10 and later no longer offer an X11 GNOME session. If you are on a current distribution and have no specific reason to use X11, Wayland is the right choice.

In the X11 era, monitor configuration sometimes required manually editing the /etc/X11/xorg.conf file. On modern Linux systems, this file is rarely present; it is typically generated only by proprietary graphics drivers, such as those from NVIDIA, under specific configurations. Unless you are troubleshooting a specific hardware issue as an advanced user, there is no reason to interact with it. The graphical Displays panel handles everything you need.