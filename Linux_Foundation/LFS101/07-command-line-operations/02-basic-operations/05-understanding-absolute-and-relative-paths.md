# Understanding Absolute and Relative Paths

## 1. Two Ways to Identify a Path

| Path Type | Starts From | Always Starts With |
| :--- | :--- | :--- |
| **Absolute** | The root directory (`/`), following the tree branch by branch to the destination | `/` |
| **Relative** | The present working directory | Never `/` |

> [!NOTE]
> Multiple slashes between directories are allowed but collapsed by the system — `////usr//bin` is treated exactly the same as `/usr/bin`.

## 2. Choosing a Style

Which style is more convenient depends on how far the destination is from the current location:

- **Relative paths** often mean less typing when the target is close by, using shortcuts like `.` (present directory), `..` (parent directory), and `~` (home directory).
- **Absolute paths** can actually be shorter and less error-prone when the target is far from the current location.

### Example

Starting from the home directory and moving to `/usr/bin`, both of these land in the same place:

```bash
# Absolute
$ cd /usr/bin

# Relative
$ cd ../../usr/bin
```

In this case, the absolute path is both shorter and less error-prone — a good reminder that neither style is always best; it depends on where you are relative to where you're going.

> [!TIP]
> If you're unsure of your current location while navigating complex directory structures, `pwd` always displays the absolute path.
