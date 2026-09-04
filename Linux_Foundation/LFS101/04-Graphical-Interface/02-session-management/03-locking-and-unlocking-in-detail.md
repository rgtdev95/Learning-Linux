# Locking and Unlocking the Screen in More Detail

## 1. What Actually Happens When You Lock

Locking does **not** suspend or shut down the machine — the session keeps running in memory exactly as it was. Only the display is replaced with the lock screen, gated by a password prompt.

## 2. Automatic Screen Lock

Most desktop environments combine two independent timers:

| Setting | Purpose | Typical Location (GNOME) |
| :--- | :--- | :--- |
| **Blank screen delay** | Turns the display off after inactivity, to save power | Settings → Power → Screen Blank |
| **Automatic lock delay** | Locks the session, either immediately when the screen blanks or after an additional delay | Settings → Privacy → Screen Lock |

> [!NOTE]
> On a laptop, prolonged inactivity can also trigger a full **suspend** after the screen locks, which is a separate mechanism (covered later in this section) — the system is no longer just displaying a lock screen, it has gone to sleep entirely.

## 3. Unlocking

1. Press a key or move the mouse to wake the display.
2. The lock screen shows the current user's name with a password field.
3. Enter the password and press Enter to return to the exact state the session was left in.

## 4. Security Note

The screen lock is authenticated through the same mechanism (PAM) as the regular login — it uses the account's normal password, not a separate lock PIN, so it's protected by whatever password policy is already in place for the account.
