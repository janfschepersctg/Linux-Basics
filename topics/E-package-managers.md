# Software management

## Package managers
One of the main points [how Linux distributions differ from each other](https://itsfoss.com/what-is-linux/) is the package management. In this part of the Linux jargon buster series, you’ll learn about packaging and package managers in Linux. You’ll learn what are packages, what are package managers and how do they work and what kind of package managers available.

## What is a package manager in Linux?

In simpler words, a package manager is a tool that allows users to install, remove, upgrade, configure and manage software packages on an operating system. The package manager can be a graphical application like a software center or a command line tool like [apt-get](https://itsfoss.com/apt-vs-apt-get-difference/) or [pacman](https://itsfoss.com/pacman-command/).

You’ll often find me using the term ‘package’ in tutorials and articles. To understand package manager, you must understand what a package is.

## What is a package?

A package is usually referred to an application but it could be a GUI application, command line tool or a software library (required by other software programs). A package is essentially an archive file containing the binary executable, configuration file and sometimes information about the dependencies.

In older days, [software used to installed from its source code](https://itsfoss.com/install-software-from-source-code/). You would refer to a file (usually named readme) and see what software components it needs, location of binaries. A configure script or makefile is often included. You will have to compile the software or on your own along with handling all the dependencies (some software require installation of other software) on your own.

To get rid of this complexity, Linux distributions created their own packaging format to provide the end users ready-to-use binary files (precompiled software) for installing software along with some [metadata](https://www.computerhope.com/jargon/m/metadata.htm) (version number, description) and dependencies.

It is like baking a cake versus buying a cake.

Around mid 90s, Debian created .deb or DEB packaging format and Red Hat Linux created .rpm or RPM (short for Red Hat Package Manager) packaging system. Compiling source code still exists but it is optional now.

To interact with or use the packaging systems, you need a package manager.

## How does the package manager work?

Please keep in mind that package manager is a generic concept and it’s not exclusive to Linux. You’ll often find package manager for different software or programming languages. There is [PIP package manager just for Python packages](https://itsfoss.com/install-pip-ubuntu/). Even [Atom editor has its own package manager](https://itsfoss.com/install-packages-in-atom/).

Since the focus in this article is on Linux, I’ll take things from Linux’s perspective. However, most of the explanation here could be applied to package manager in general as well.

I have created this diagram (based on SUSE Wiki) so that you can easily understand how a package manager works.
![Linux Package Manager Explanation](https://i2.wp.com/itsfoss.com/wp-content/uploads/2020/10/linux-package-manager-explanation.png?resize=800%2C450&ssl=1)
Almost all Linux distributions have software repositories which is basically collection of software packages. Yes, there could be more than one repository. The repositories contain software packages of different kind.

Repositories also have metadata files that contain information about the packages such as the name of the package, version number, description of package and the repository name etc. This is what you see if you use the [apt show command](https://itsfoss.com/apt-search-command/) in Ubuntu/Debian.

Your system’s package manager first interacts with the metadata. The package manager creates a local cache of metadata on your system. When you run the update option of the package manager (for example apt update), it updates this local cache of metadata by referring to metadata from the repository.

When you run the installation command of your package manager (for example apt install package_name), the package manager refers to this cache. If it finds the package information in the cache, it uses the internet connection to connect to the appropriate repository and downloads the package first before installing on your system.

A package may have dependencies. Meaning that it may require other packages to be installed. The package manager often takes care of the dependencies and installs it automatically along with the package you are installing.

Similarly, when you remove a package using the package manager, it either automatically removes or informs you that your system has unused packages that can be cleaned.

Apart from the obvious tasks of installing, removing, you can use the package manager to configure the packages and manage them as per your need. For example, you can [prevent the upgrade of a package version](https://itsfoss.com/prevent-package-update-ubuntu/) from the regular system updates. There are many more things your package manager might be capable of.

## Working with yum / dnf (RPM)
https://github.com/uidmehdi/cheat-sheets/blob/master/Yum.md

## Sources
https://itsfoss.com/package-manager/
