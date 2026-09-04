Office Applications

For everyday document creation, spreadsheet work, and presentations, LibreOffice(opens in a new tab) is the standard office suite on Linux. It is open source, actively maintained, pre-installed on most major distributions, and available at no cost. LibreOffice originated in 2010 as a fork of OpenOffice and has since become the most mature and widely used office suite in the Linux ecosystem.

LibreOffice includes the following applications:

•
Writer - word processor

•
Calc - spreadsheet application

•
Impress - presentation tool

•
Draw - vector graphics and diagram editor

•
Base - database frontend

•
Math - formula editor for creating mathematical and scientific notation

LibreOffice can read and write Microsoft Office file formats such as .docx, .xlsx, .pptx, allowing you to exchange documents with Windows and macOS users without compatibility issues in most cases. Complex files with advanced formatting or macros may sometimes need minor adjustments, but everyday documents typically convert reliably.



LibreOffice Applications

While LibreOffice is the primary choice, a notable alternative worth knowing about is ONLYOFFICE(opens in a new tab) Desktop Editors, a free, open source office suite that has gained a strong following in the Linux community. ONLYOFFICE is particularly valued for its high-fidelity handling of Microsoft Office formats: it tends to preserve complex formatting, styles, and document structure more accurately than LibreOffice when working with .docx, .xlsx, and .pptx files. If you regularly exchange documents with Windows or macOS users who work in Microsoft Office, ONLYOFFICE is worth evaluating alongside LibreOffice. It is available in modern packaging formats, including Flatpak and Snap, and can be installed directly from the software center on Ubuntu and Fedora, or downloaded from the ONLYOFFICE website.

Beyond installable office suites, for cloud-based work, Google Docs, Google Sheets, and Microsoft Office 365 all run in any Linux browser, giving Linux users full access to those platforms without any additional software.


Development Applications

Linux has been the platform of choice for software development for decades, and it shows. A complete, professional-grade development environment is available out of the box or within a few package installations, at no cost.

Select the plus (+) sign next to the option name to learn about key development tools available on Linux.


Editors
VS Code (Visual Studio Code) is Microsoft's popular code editor, available as a native Linux package. While the underlying project is open source, Microsoft's official distributed binaries include proprietary components and telemetry. An entirely open source alternative, VSCodium, is also widely available and provides the same functionality without the proprietary additions.

vim and emacs are powerful, highly configurable terminal-based editors with steep learning curves but exceptional efficiency once mastered. Both are covered later in this course.


Compilers, Interpreters, and Runtimes
GCC (GNU Compiler Collection) and Clang are the standard compilers for C and C++, available in all distribution repositories.

Python comes pre-installed on virtually every Linux distribution, as the system itself relies on Python for internal scripts and package management tools. This is notably different from Windows and macOS, where Python must be installed separately.

Compilers and runtimes for all languages in active use, including Go, Rust, Java, Ruby, and Node.js, are available in standard repositories.


Debuggers
GDB (GNU Debugger) is the standard debugger for C, C++, and several other languages. Multiple graphical frontends are available.

Valgrind is a tool for detecting memory management errors and profiling application performance.


Version Control
Git is the universal standard for source code version control, available in the repositories of every Linux distribution and installable with a single command. Integrates seamlessly with hosting platforms, including GitHub and GitLab.

Apache Subversion (SVN) is an older centralized version control system still in use in some enterprise and legacy environments.


Containers
Docker is the most widely used platform for building, running, and managing containers. Linux is the native environment for containerization, and Docker runs with full native performance on Linux without the virtualization layer required on Windows and macOS.

Podman is a daemonless container engine that is compatible with Docker commands and is the default container tool on Fedora and RHEL. It is increasingly preferred in enterprise environments for its improved security model.


Integrated Development Environments (IDEs)
Eclipse is a mature, extensible IDE with strong support for Java and C/C++.

Visual Studio Code also functions as a lightweight IDE with extensions covering most languages and frameworks.

JetBrains tools (IntelliJ IDEA, PyCharm, CLion, and others) are professional-grade IDEs available on Linux, with free community editions for many products.

While other operating systems now offer easier access to development tools than they once did, such as macOS's Xcode Command Line Tools or Windows Subsystem for Linux (WSL), Linux remains the native environment for these toolchains, offering seamless integration directly through the system's package manager without additional compatibility layers.