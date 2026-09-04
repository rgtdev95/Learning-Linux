# Locating Applications

## 1. Browsing by Category

Applications are organized into functional categories within the application launcher, making it easy to browse by type — **Office**, **Internet**, **Sound & Video**, **Utilities**, and so on. This is consistent across GNOME, KDE, and Cinnamon, though the exact category names may vary slightly between them.

## 2. Searching for an Application

If an application can't be found by browsing, the search function is the quickest alternative. On every major desktop environment, opening the application launcher and typing a name or keyword locates what you need almost immediately.

> [!NOTE]
> Search typically covers application names and descriptions, and in some cases file contents as well.

## 3. Where This Comes From (Supplementary)

Application menus are generated from `.desktop` files, not hand-maintained lists:

| Location | Scope |
| :--- | :--- |
| `/usr/share/applications/` | System-wide applications, available to every user |
| `~/.local/share/applications/` | Applications installed or added for the current user only |

> [!NOTE]
> If an installed program doesn't show up when browsing or searching, the most common cause is a missing or malformed `.desktop` file in one of these locations.
