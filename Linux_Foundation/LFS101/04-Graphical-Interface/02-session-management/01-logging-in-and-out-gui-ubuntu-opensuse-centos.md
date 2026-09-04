# Logging In and Logging Out Using the GUI (Ubuntu, openSUSE, CentOS)

The graphical login/logout flow is nearly identical across the three distribution families this course covers, because all of them present a GNOME-based greeter by default. The differences are cosmetic, not conceptual.

## 1. The Common Flow

1. The **display manager** (GDM3 on Ubuntu, GDM on Fedora/RHEL/CentOS/openSUSE) presents the greeter with a list of local accounts.
2. Selecting a user prompts for a password. A gear icon lets you pick the session type (**Wayland** by default, with an **Xorg** fallback on most systems).
3. After authenticating, the GNOME desktop loads (first login may show a one-time welcome/setup screen).
4. Logging out is done from the system menu in the top-right corner of the top bar → power icon → **Log Out**.

## 2. Distribution Notes

| Distribution | Display Manager | Notes |
| :--- | :--- | :--- |
| **Ubuntu** | GDM3 | Power menu lists Suspend / Restart / Power Off / Log Out / Switch User individually. |
| **openSUSE** | GDM | Same GNOME shell layout as Ubuntu and CentOS; menu wording matches upstream GNOME rather than a distro-specific skin. |
| **CentOS** | GDM | Power options are grouped under a **Power off / Log out** submenu rather than listed flat. |

> [!NOTE]
> Because Ubuntu, openSUSE, and CentOS in this course all run stock **GNOME**, the login/logout experience is driven by GNOME Shell itself — the underlying distribution mostly changes branding (backgrounds, default icon theme) rather than the workflow.

See [03-system-startup-and-logging-in-out.md](../01-graphical-desktop/03-system-startup-and-logging-in-out.md) for the walkthrough of the Ubuntu and CentOS login/logout demo.
