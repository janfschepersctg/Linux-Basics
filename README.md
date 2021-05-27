# CTG Devops Academy: linux

## Introduction
Everyone should start it's learning journey somewhere. *But where the heck do I start?* 

With this course I've build a "roadmap" for making an acquaintance with the different pieces of the Linux operating system and explaining how they work together. 

I've compiled a list of topics a Linux engineer should consider 'basic' knowledge. 
Even then, each topic in this course barely scratches the surface and a lot of stuff didn't even make the cut (yet).

I'm hoping this repository can be useful throughout the start of your Linux journey. Giving u something to fallback to when in doubt, when you're not sure how to even start solving a problem or just because you're getting hooked on Linux and want to learn more. 

## Topics
For each topic, I've search the internet of relevant sources and bundled them together (...so you don't have to)!
1. [Systemd](topics/A-Systemd.md)
2. [Access control](topics/B-Access-control.md)
3. [Process control](topics/C-Process-control.md)
4. [Moving around](topics/D-Basic-navigation.md)
5. [Working with files](topics/D-File-Manipulation.md)
6. [Common directories in linux](topics/D-Linux-common-folders.md)
7. [Package managers](topics/E-package-managers.md)
8. [Repositories](topics/E-Repositories.md)
9. [Shell basics](topics/F-Shell-basics.md)
10. [Bash scripts](topics/F-bash-scripts.md)
11. [Vim](topics/F-vim.md)
12. [Pipe](topics/G-Pipe.md)
13. [Text Filtering](topics/G-Text-filtering.md)
14. [Linux logging: where and how to read them](topics/H-Logging.md)
15. [Network troubleshooting](topics/I-Network-troubleshooting.md)
16. [Iptables as firewall](topics/J-Iptables.md)

## Environment for playing around
While following this course, we are gonna use a virtual environment for messing around without doing any harm.
### Prerequisites
On your working machine, make sure you have installed recent versions of:

- [VirtualBox](https://virtualbox.org/)
- [Vagrant](https://vagrantup.com/)
- [Git](https://git-scm.com/) and for Windows hosts also Git Bash. If you install Git with default settings (i.e. always click "Next" in the installer), you should be fine.
- Ansible (only on Mac/Linux)

### Getting started

- creating our virtual environment: `vagrant up`
- deleting our virtual environment: `vagrant destroy -f`
- SSH to our virtual environment: `vagrant ssh srv01`

## Contributors

- [Bert Van Vreckem](https://github.com/bertvv/): Maintainer of the vagrant skeleton on which this project is based.
- All the people who took their time writing the resources I've been copying. In each topic, you'll find the relevant source url's.


