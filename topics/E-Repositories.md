# Software management

## Repositories
A Linux repository is a storage location from which your system retrieves and installs OS updates and applications. Each repository is a collection of software hosted on a remote server and intended to be used for installing and updating software packages on Linux systems. When you run commands such as `sudo yum update` or `sudo yum upgrade`, you may be pulling package information and package updates from a number of repositories.

Repositories contain thousands of programs. Standard repositories provide a high degree of security, since the software included is thoroughly tested and built to be compatible with a particular distribution and version. So, you can expect the updates to occur with no unexpected "side effects."

Repositories may be standard or non-standard. Once a non-standard repository has been added to your system's list of repositories, the system can install software from it, as well as from the standard ones; otherwise, it cannot. In general, adding a non-standard repository is a simple step. 

```
dnf config-manager --add-repo _repository_url_
```
You should be careful, however, when adding a non-standard repository to be sure that it has been tested and is known to work on your particular system.

### Common commands (RPM)
On RedHat, Fedora and similar systems, you would use a command like the one shown below to view the repositories that your update commands use. Note that we're using the **dnf** command in this example. This is the replacement for the older **yum** command.

```$ sudo dnf repolist
Last metadata expiration check: 0:18:37 ago on Sat 15 Sep 2018 12:28:02 PM EDT.
repo id        repo name                            status
*fedora        Fedora 28 - x86_64                   57,327
*updates       Fedora 28 - x86_64 - Updates         18,739
```

The **status** field in the output above represents the number of packages in each of the repositories. If you add the "all" specification, you will also see disabled (not used) repositories. In the command below, we see that quite a number of other repositories are disabled.
```
$ sudo dnf repolist all
Last metadata expiration check: 0:19:39 ago on Sat 15 Sep 2018 12:28:02 PM EDT.
repo id                            repo name                        status
*fedora                            Fedora 28 - x86_64               enabled: 57,327
fedora-cisco-openh264              Fedora 28 openh264 (From Cisco)  disabled
fedora-cisco-openh264-debuginfo    Fedora 28 openh264 (From Cisco)  disabled
fedora-debuginfo                   Fedora 28 - x86_64 - Debug       disabled
fedora-source                      Fedora 28 - Source               disabled
*updates                           Fedora 28 - x86_64 - Updates     enabled: 18,739
updates-debuginfo                  Fedora 28 - x86_64 - Updates - D disabled
updates-source                     Fedora 28 - Updates Source       disabled
updates-testing                    Fedora 28 - x86_64 - Test Update disabled
updates-testing-debuginfo          Fedora 28 - x86_64 - Test Update disabled
updates-testing-source             Fedora 28 - Test Updates Source  disabled
```
Enabling a repository can be done with a command like this:
```
dnf config-manager --set-enabled repository_url
```
You can also add repositories fairly easily with commands like this:
```
dnf config-manager --add-repo http://www.example.com/example.repo
```

## Sources
https://www.networkworld.com/article/3305810/how-to-list-repositories-on-linux.html
