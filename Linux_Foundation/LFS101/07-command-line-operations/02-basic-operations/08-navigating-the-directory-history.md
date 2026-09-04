# Navigating the Directory History

## 1. Quick Return: `cd -`

The `cd` command remembers the last directory you were in, and `cd -` returns you there immediately.

## 2. The Directory Stack: `pushd`, `popd`, `dirs`

To remember more than just the last directory, use `pushd` instead of `cd` to change directories — this pushes your starting directory onto a list, the **directory stack**.

| Command | Effect |
| :--- | :--- |
| `pushd <path>` | Changes to `<path>`, pushing the current directory onto the stack |
| `popd` | Returns to the most recently pushed directory, removing it from the stack |
| `dirs` | Displays the current contents of the directory stack |

> [!NOTE]
> `popd` walks the stack in reverse order — the most recently visited directory is the first one retrieved.

## 3. Demo Walkthrough (Gentoo)

This demo uses Gentoo, but the behavior is identical on any distribution.

1. Start in `/tmp`, confirmed with `pwd`.
2. Change to `/usr/local` with a plain `cd` — this move isn't tracked by the directory stack.
3. From `/usr/local`, start using `pushd`:
   - `pushd /tmp` → now in `/tmp`; `/usr/local` is pushed onto the stack.
   - `pushd /boot` → now in `/boot`; the stack grows.
   - `pushd /` → now in `/`; the stack grows again.
4. `dirs` shows the full stack — `/`, `/boot`, `/tmp`, `/usr/local` — everywhere visited, in order.
5. `popd` → back to `/boot`.
6. `popd` again → back to `/tmp`.
7. `popd` a third time → back to `/usr/local`, where the pushing began. The stack is now empty.

> [!NOTE]
> The stack only tracks directories entered via `pushd`. Since `/usr/local` was originally reached with a plain `cd` rather than `pushd`, it was never itself pushed onto the stack — it's simply where the pushing started, and where the stack unwinds back to.

## Key Takeaway

`pushd` / `popd` / `dirs` remember an entire trail of directories, not just the single previous one that `cd -` remembers — useful when working across several directories and needing to retrace your steps precisely.
