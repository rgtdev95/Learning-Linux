# Other Documentation Sources

Beyond the man pages, the GNU Info system, and shell help commands, Linux offers several other places to find documentation: desktop graphical help systems, files bundled directly inside installed software packages, and online community resources.

## 1. Graphical Help Systems

Every major Linux desktop environment includes a graphical help application, usually reachable from the applications menu and marked with a question-mark "Help" icon. These apps provide guides for the desktop environment itself, and can often display man and info pages in a nicely formatted, clickable form too.

Rather than hunting for the right menu item, the help browser can also be launched straight from a terminal:

| Desktop Environment | Command |
| :--- | :--- |
| GNOME | `yelp` (also available as `gnome-help`) |
| KDE | `khelpcenter` |

> [!NOTE]
> Just as in Windows and macOS, pressing **F1** in many Linux desktop applications opens the app's help page directly — the fastest way to access an application's documentation, though support varies, so don't be surprised if F1 does nothing in certain programs.

## 2. Package Documentation

When software is installed, documentation files ship directly alongside the executable files — upstream documentation from the developers, as well as specific notes from the distribution's maintainers.

These files live under `/usr/share/doc`, organized into subdirectories named after each package — for example, `/usr/share/doc/bash/`. Browsing these folders is a great way to discover README files, changelogs, and sample configuration files not included in standard man pages.

## 3. Online Resources

There's no shortage of Linux documentation online — a quick search on almost any topic turns up more than can be read in one sitting.

One widely recommended starting point is **"The Linux Command Line"** by William Shotts, a free, downloadable book available under a Creative Commons license that many learners in this course have praised.

Each distribution also maintains its own documentation, along with community forums and wikis:

- Ubuntu Documentation
- CentOS Stream Documentation
- openSUSE Documentation
- Gentoo Documentation
- Fedora Documentation

> [!NOTE]
> General web searches will also surface blog posts, forum and mailing-list threads, news articles, and more from across the internet.
