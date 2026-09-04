# Switching Users in Ubuntu

## Demo Walkthrough

Starting point: logged in as the Linux Foundation `student` user.

1. Click the system menu in the **upper-right corner**, then click the **power button** icon. This drops down a menu that includes **Log Out** and **Switch User**.
2. Rather than logging out, select **Switch User** to leave the `student` session alive and come back to it later.
3. This returns to the **greeter screen**. Log in as `bob` (his own login credentials are required).
4. In `bob`'s session, open a terminal and work normally, just as in any other session.
5. To switch again, repeat the same steps: upper-right corner → power button → **Log Out** or **Switch User**.
6. Selecting **Switch User** and logging back in as `student` returns to the exact terminal window and work left behind — including anything still actively running in the background, such as jobs that were kicked off before switching away.
7. Switching back to `bob` shows the same login prompt as before, confirming his session was preserved too.
8. Finally, logging out as `bob` and logging back in as `student` completes the loop.

## Key Takeaway

Both sessions — `student`'s and `bob`'s — stayed alive and fully intact the entire time, including background jobs, even while switching back and forth between them. **Switch User** never closes a session; only **Log Out** does.

> [!NOTE]
> This builds directly on the general [Switching Users](04-switching-users.md) concept — the mechanics (system menu → power icon → Switch User → greeter) are the same ones introduced there, applied here on Ubuntu with the `student` and `bob` accounts.
