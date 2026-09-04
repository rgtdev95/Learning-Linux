# Logging In and Out (Demo Notes)

This section demonstrates logging in and out of a Linux desktop, using Ubuntu (GNOME) and CentOS (GNOME) as examples.

## 1. The Greeter Screen

- On startup, the **greeter** (login screen) lists the available local accounts — in the demo: the Linux Foundation student account, `alice`, and `bob`.
- Selecting a username prompts for that user's password.

## 2. Choosing a Session Type

- Before entering the password, a **gear icon** on the login screen lets you choose the session type.
- On Ubuntu, the default is **Wayland**; an **Ubuntu on Xorg** option is available for backward compatibility.
- CentOS presents a few more session options, but **Wayland** remains the standard choice.

## 3. First Login

- The first time a user logs in, GNOME shows a **welcome/setup screen**. It can be dismissed (e.g., "No, thanks") to go straight to the desktop.

## 4. Using the Desktop

- Installed applications are available from the **Activities** overview / application launcher.
- Opening a **Terminal** gives access to the shell, where standard commands (`ls`, `cd /usr/bin`, etc.) work as expected.

## 5. Logging Out

- The logout controls are in the **top-right corner** of the top bar.
- Clicking the power icon opens a menu with several options:
  - **Suspend**
  - **Restart**
  - **Power Off**
  - **Log Out**
  - **Switch User**
- **Switch User** keeps the current user's session running in the background and returns to the greeter so another person can log in — useful when someone else needs quick access to the machine without ending your session.
- Choosing **Log Out** shows a confirmation with a countdown (60 seconds in the demo) before logging out automatically.
- Logging out returns you to the greeter screen, ready for the next login.

> [!NOTE]
> Open applications (like a terminal window) do not block logout. The demo intentionally left a terminal open when logging out `bob`, and the system logged out normally regardless.

## 6. Distribution Differences

The overall flow is nearly identical across distributions; only minor UI differences appear:

| | Ubuntu (GNOME) | CentOS (GNOME) |
| :--- | :--- | :--- |
| Power menu | Power icon with individual options | **Power off / Log out** submenu |
| Session type default | Wayland (Xorg fallback available) | Wayland (a few additional options available) |
