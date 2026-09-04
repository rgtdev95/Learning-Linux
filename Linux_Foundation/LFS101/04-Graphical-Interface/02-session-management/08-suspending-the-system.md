# Suspending the System

## 1. What Suspend Does

**Suspend** (sleep) keeps the current session in RAM while powering down almost everything else — display, disks, most peripherals — making it much faster to resume than a full shutdown and reboot, since nothing needs to reload.

## 2. How to Suspend on GNOME

The method varies slightly between distributions:

| Distribution | How to Suspend |
| :--- | :--- |
| Most GNOME-based distributions | Click and hold the power icon in the system menu for a moment, then release — this reveals an alternative suspend icon (two vertical lines); click it to suspend |
| **Ubuntu** | A dedicated **Suspend** option may appear directly in the power menu alongside Power Off and Restart, depending on the version |
| **Fedora** | Hold **Alt** while the power menu is open to swap the **Power Off** option for a **Suspend** option |

> [!TIP]
> If you're unsure which method applies to your distribution, the quickest approach is to open the system menu and look for a suspend or sleep option — it's present on all current distributions, even if it takes a slightly different form.

## 3. Waking the System

Press any key on the keyboard or move the mouse to wake a suspended system. It resumes within a few seconds and presents the **lock screen**, exactly as though the session had been locked manually. Entering the password returns to the session exactly as it was left.

> [!NOTE]
> **Suspend** differs from **hibernate**, which saves the session to disk instead of RAM and draws no power while off, at the cost of a slower resume. Not every distribution enables hibernate by default — it depends on having a swap area large enough to hold the contents of RAM.
