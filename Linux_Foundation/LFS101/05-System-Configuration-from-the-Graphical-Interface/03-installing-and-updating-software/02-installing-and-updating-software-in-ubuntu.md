# Installing and Updating Software in Ubuntu (Demo Notes)

Most experienced Linux system administrators use the command line for package management — installing, removing, or updating packages. However, every major distribution also includes one or more graphical tools for software management. This demo walks through three of them on Ubuntu.

## 1. GNOME Software

Common on all GNOME-based distributions. If not already installed, it can be added via the GNOME Software package.

- Opens by default to the **Explore** tab, organized into categories such as Create, Socialize, Work, Learn, Play, and Develop, plus an Editor's Choice section.
- Browsing a category (e.g., **Develop**) shows an alphabetical, scrollable list of matching applications.
- The **back arrow** (upper-left) returns to the main Explore screen from any category.
- The **Installed** tab lists already-installed software alphabetically.
- The **Updates** tab shows pending updates (e.g., a browser needing an update), with the option to **Update All** or update individual applications.

### Searching and Installing (Cheese Example)

1. Click the **magnifying glass** icon in Explore to search — e.g., "Cheese" (a webcam photo/video application).
2. Search results may show multiple packaging formats for the same app — in this case, a **Snap** and a **Debian package**. This demo uses the Debian package, consistent with the packaging this course focuses on.
3. Selecting the app opens a detail page with a description, download size, and an **Install** button.
4. Installing requires **authentication** — an administrator password, since the demo account has administrative privileges.
5. Once installed, an **Uninstall** button replaces Install; uninstalling prompts a confirmation ("Are you sure you want to uninstall this?") before removing it.

## 2. Ubuntu App Center

Visually and functionally very similar to GNOME Software, with its own set of browsable categories.

- A search bar sits at the top-center; searching "Cheese" again shows results broken into separate **Snap** and **Debian package** sections.
- Selecting a result shows a screenshot and description alongside the same **Install** / **Uninstall** workflow as GNOME Software.

## 3. Synaptic Package Manager

An older, more detailed tool, also requiring authentication to make changes.

- Packages are organized into categories in a sidebar on the left.
- **Search** (upper-right) can match by name and/or description.
- Right-clicking a package offers **Mark for Installation**, plus a **Properties** view showing version, download size, the full list of **dependencies**, installed files, and versions.
- Marking a package for installation queues it; performing the actual install then pulls in any needed dependencies (libraries, utilities) automatically.
- This gives more granular, package-level control than the app-store-style tools — useful once you want to manage software at a more detailed level.

## 4. Summary

All three tools provide a broadly similar, approachable way to manage software graphically — a good starting point while first learning Linux. Availability follows the distribution:

| Distribution | Typical Graphical Tools |
| :--- | :--- |
| **Ubuntu** | App Center, Synaptic Package Manager, GNOME Software |
| **Other GNOME-based distributions** | GNOME Software |

> [!NOTE]
> If GNOME Software isn't installed on a given system, it can be added as a package — but doing so requires the command line.
