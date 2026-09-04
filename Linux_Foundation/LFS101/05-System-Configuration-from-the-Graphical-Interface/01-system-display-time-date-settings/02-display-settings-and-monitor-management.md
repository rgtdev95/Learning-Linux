# Display Settings and Monitor Management

## 1. Adjusting Your Display

To manage how the system presents information on screen, navigate to **Settings → Displays**. On some distributions and older GNOME versions, this may instead be found under **Settings → Devices → Displays**. It's also reachable by right-clicking anywhere on the desktop and selecting **Display Settings**.

Most current distributions, including Ubuntu 24.04 and Fedora, automatically detect and select the **native resolution** of the monitor, which produces the sharpest image.

> [!NOTE]
> While the resolution can be overridden, selecting a non-native resolution typically results in a blurry or stretched interface and isn't recommended unless there's a specific reason to do so.

For displays that support higher refresh rates, the **Refresh Rate** dropdown allows selecting a higher frequency (such as 120Hz or 144Hz) for a smoother, more fluid visual experience — particularly relevant for gaming or working with animations and video.

## 2. Fractional Scaling

To enable fractional scaling on GNOME, open **Settings → Displays** and toggle on **Fractional Scaling** if it isn't already active. Intermediate scale options then appear in the scale selector.

## 3. Night Light

**Night Light** shifts the display toward warmer tones during the evening — lighting that's easier on the eyes at night than the display's normal color temperature. It's configured from the same Displays panel.

## 4. Configuring Multiple Monitors

When an additional monitor is connected, the system typically detects it and extends the desktop automatically. The Displays panel provides a visual map of all connected screens, which can be interacted with directly:

- **Arrange monitors** by dragging the screen icons to match their physical positions on the desk — this ensures the mouse cursor moves logically from one screen to the next.
- **Designate a Primary Display** — the monitor that shows the top bar, including the Activities button and system clock. Dock behavior on secondary displays may vary by distribution; on Ubuntu, the dock can be configured to appear on all displays or only the primary one, in **Settings → Ubuntu Desktop**.

### Display Modes

| Mode | Behavior |
| :--- | :--- |
| **Join Displays** | Extends the desktop across all monitors into a single continuous workspace — the standard working configuration |
| **Mirror** | Shows identical content on all connected displays — the typical choice for presentations |
| **Single Display** | Disables all but the selected monitor |

> [!TIP]
> Applying a new display configuration brings up a confirmation dialog with a 15-second countdown. If **Keep Changes** isn't selected within that time, the system automatically reverts to the previous working configuration — a safety mechanism that prevents being left with an unusable or blank display if a setting doesn't work as expected.

## 5. A Note on the Underlying Display Infrastructure

As discussed in [How the Graphical Desktop Loads](../../04-graphical-interface/01-graphical-desktop/01-how-graphical-desktop-loads.md), Linux uses a **display server** to draw windows and manage keyboard/mouse input. Current distributions — Ubuntu 22.04+, Fedora, RHEL — use **Wayland** as the default, which handles modern features like fractional scaling and multi-monitor configuration more reliably than its predecessor.

The legacy **X11** session remains available on Ubuntu 24.04 and some other current distributions, primarily for compatibility with older hardware or specific enterprise environments that require it. It's being phased out: Ubuntu 25.10 and later no longer offer an X11 GNOME session. On a current distribution with no specific reason to use X11, Wayland is the right choice.

> [!NOTE]
> In the X11 era, monitor configuration sometimes required manually editing `/etc/X11/xorg.conf`. On modern Linux systems this file is rarely present — it's typically generated only by proprietary graphics drivers (such as NVIDIA's) under specific configurations. Unless troubleshooting a specific hardware issue as an advanced user, there's no reason to interact with it directly; the graphical Displays panel handles everything needed.
