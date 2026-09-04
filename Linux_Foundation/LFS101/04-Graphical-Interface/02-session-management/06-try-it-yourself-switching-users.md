# Try-It-Yourself: Switching Users in Ubuntu

> [!NOTE]
> This is a hands-on exercise. The steps below reflect the general pattern for this kind of lab in the course — walk through them on your own VM to confirm the behavior described in the previous lessons.

## Suggested Steps

1. **Log in** as your primary user (e.g., `alice`).
2. Open a couple of applications (a terminal, a text editor, a browser) so there's visible session state to check later.
3. Open the system menu (top-right corner) and select **Switch User**.
4. At the greeter, log in as a second account (e.g., `bob`). Note that this does **not** prompt to close `alice`'s session.
5. As `bob`, open a different application, then switch back: system menu → **Switch User**.
6. At the greeter, select `alice` again and enter her password.
7. **Confirm**: the applications opened in step 2 should still be open, exactly as left — proving the first session stayed alive the entire time.

## What to Observe

- Both users' sessions can run concurrently; check with `who` or `w` in a terminal to see multiple logged-in sessions at once.
- Resource usage (`top` or the System Monitor) will reflect two full desktop sessions running simultaneously.
