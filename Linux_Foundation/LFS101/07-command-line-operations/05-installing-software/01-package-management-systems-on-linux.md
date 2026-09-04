# Package Management Systems on Linux

## 1. What Package Management Handles

The core parts of a Linux distribution, and most of its add-on software, are installed through a **Package Management System**. Each package contains the files and instructions needed to ensure one software component works correctly and cooperates with the other components that make up the system. Packages can also depend on one another — a web application written in Python, for example, requires the appropriate Python packages to be installed first.

There are two broad families of package managers in wide use: those based on **Debian**, and those that use **RPM** as their low-level package manager. The two systems are incompatible, but broadly speaking, they provide the same essential features and meet the same needs. A few more specialized distributions use other systems as well.

This section covers installing, removing, and searching for packages from the command line using these two package management systems.

## 2. Package Managers: Two Levels

Both package management systems operate on two distinct levels:

| Level | Role |
| :--- | :--- |
| **Low-level** (`dpkg`, `rpm`) | Handles the details of unpacking individual packages, running their installation scripts, and getting the software installed correctly |
| **High-level** (`apt`, `dnf`, `zypper`) | Works with groups of packages, downloads them from software repositories, and resolves dependencies |

Most of the time, users work only with the high-level tool, which calls the low-level tool as needed.

> [!NOTE]
> Dependency resolution is one of the most important features of the high-level tool: it automatically finds and installs everything a package needs. Be aware, though, that installing a single package can sometimes pull in dozens or even hundreds of dependencies.

## 3. High-Level Tools by Distribution Family

Each distribution family has its own high-level package manager, but they all play the same role: downloading packages from repositories, resolving dependencies, and calling the appropriate low-level tool (`dpkg` or `rpm`) behind the scenes. Once one is understood, the others feel familiar — the concepts are the same, and only the command names and options differ.

| Tool | Distribution Family |
| :--- | :--- |
| **apt** (Advanced Packaging Tool) | Debian-based systems, such as Debian and Ubuntu. Also serves as the backend for graphical tools like the Ubuntu Software Center and Synaptic, but its native interface is the command line, through `apt` (or the older `apt-get`) and `apt-cache`. |
| **dnf** | RPM-based systems in the Red Hat family, such as Fedora, RHEL, and CentOS Stream |
| **zypper** | The SUSE/openSUSE family (also RPM-based); lets you manage repositories from the command line and closely resembles `dnf` |

## 4. Command Reference

In the tables below, `foo` is the name of a package, and `foo.rpm` / `foo.deb` are package files on disk.

### Low-Level Tools

| Operation | `rpm` (Fedora/RHEL/openSUSE) | `dpkg` (Debian/Ubuntu) |
| :--- | :--- | :--- |
| Install a package from a file | `rpm -i foo.rpm` | `dpkg --install foo.deb` |
| Update a package from a file | `rpm -U foo.rpm` | `dpkg --install foo.deb` |
| Remove a package | `rpm -e foo` | `dpkg --remove foo` |
| List all installed packages | `rpm -qa` | `dpkg --list` |
| Show information about a package | `rpm -qi foo` | `dpkg -s foo` |
| List the files a package installed | `rpm -ql foo` | `dpkg -L foo` |
| Get information on a package | `rpm -qil foo` | `dpkg --listfiles foo` |
| Find which package a file belongs to | `rpm -qf file` | `dpkg --search file` |

### High-Level Tools

| Operation | `dnf` (Fedora/RHEL) | `zypper` (openSUSE) | `apt` (Debian/Ubuntu) |
| :--- | :--- | :--- | :--- |
| Install a package + dependencies | `dnf install foo` | `zypper install foo` | `apt install foo` |
| Remove a package + unused dependencies | `dnf remove foo` | `zypper remove foo` | `apt remove foo` then `apt autoremove` |
| Update a package + dependencies | `dnf upgrade foo` | `zypper update foo` | `apt install foo` |
| Update the entire system | `dnf upgrade` | `zypper update` | `apt upgrade` |
| List all installed packages | `dnf list installed` | `zypper search --installed-only` | `apt list --installed` |
| Search for packages named foo | `dnf list "foo"` | `zypper search foo` | `apt search foo` |
| List all available packages | `dnf list available` | `zypper packages` (or `zypper pa`) | `apt list` |

## 5. Important Notes

- On Debian-based systems, `apt install foo` serves double duty: it installs `foo` if it isn't present, and upgrades it to the newest available version if it is — which is why the same command appears for both installing and updating.
- Before upgrading on Debian/Ubuntu, always run `apt update` first. `apt` works from a locally cached list of available packages, and `apt update` refreshes that list from the repositories; `apt upgrade` then acts on it. Skipping `apt update` means `apt upgrade` may not see the newest available versions, even though they exist.
- On Debian/Ubuntu, `apt remove foo` deletes the package but can leave behind dependencies that were installed alongside it and are no longer needed. Running `apt autoremove` afterward cleans these up. To also delete the package's leftover configuration files, use `apt purge foo` instead of `apt remove foo`.
