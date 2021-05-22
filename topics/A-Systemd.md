
# Systemd

## Introduction

`systemd` is an init system and system manager that has widely become the new standard for Linux distributions. Due to its heavy adoption, familiarizing yourself with `systemd` is well worth the trouble, as it will make administering servers considerably easier. Learning about and utilizing the tools and daemons that comprise `systemd` will help you better appreciate the power, flexibility, and capabilities it provides, or at least help you to do your job with minimal hassle.

## The Linux Boot Process and systemd

To better understand what is meant by an initialization system, this section provides a high-level overview of the Linux boot process.

Linux requires an initialization system during its boot and startup process. At the end of the [boot process](https://en.wikipedia.org/wiki/Linux_startup_process), the Linux kernel loads systemd and passes control over to it and the startup process begins. During this step, the kernel initializes the first [user space](https://en.wikipedia.org/wiki/User_space) process, the systemd init process with process ID 1, and then goes idle unless called again. systemd prepares the [user space](https://en.wikipedia.org/wiki/User_space) and brings the Linux host into an operational state by starting all other processes on the system.

Below is a simplified overview of the entire Linux boot and startup process:

1.  The system powers up. The BIOS does minimal hardware initialization and hands over control to the boot loader.
2.  The boot loader calls the kernel.
3.  The kernel loads an initial RAM disk that loads the system drives and then looks for the root file system.
4.  Once the kernel is set up, it begins the systemd initialization system.
5.  systemd takes over and continues to mount the host’s file systems and start services.

## Basic Unit Management

The basic object that `systemd` manages and acts upon is a “unit”. Units can be of many types, but the most common type is a “service” (indicated by a unit file ending in `.service`). To manage services on a `systemd` enabled server, our main tool is the `systemctl` command.

All of the normal init system commands have equivalent actions with the `systemctl` command. We will use the `httpd.service` unit to demonstrate (you’ll have to install httpd with your package manager to get this service file).

For instance, we can start the service by typing:

```bash
sudo systemctl start httpd.service
```

We can stop it again by typing:

```bash
sudo systemctl stop httpd.service
```

To restart the service, we can type:

```bash
sudo systemctl restart httpd.service
```

To attempt to reload the service without interrupting normal functionality, we can type:

```bash
sudo systemctl reload httpd.service
```

## Enabling or Disabling Units

By default, most `systemd` unit files are not started automatically at boot. To configure this functionality, you need to “enable” to unit. This hooks it up to a certain boot “target”, causing it to be triggered when that target is started.

To enable a service to start automatically at boot, type:

```bash
sudo systemctl enable httpd.service
```

If you wish to disable the service again, type:

```bash
sudo systemctl disable httpd.service
```

## Getting an Overview of the System State

There is a great deal of information that we can pull from a `systemd` server to get an overview of the system state.

For instance, to get all of the unit files that `systemd` has listed as “active”, type (you can actually leave off the `list-units` as this is the default `systemctl` behavior):

```bash
systemctl list-units
```

To list all of the units that `systemd` has loaded or attempted to load into memory, including those that are not currently active, add the `--all` switch:

```bash
systemctl list-units --all
```

To list all of the units installed on the system, including those that `systemd` has not tried to load into memory, type:

```bash
systemctl list-unit-files
```

## Viewing Basic Log Information

A `systemd` component called `journald` collects and manages journal entries from all parts of the system. This is basically log information from applications and the kernel.

To see all log entries, starting at the oldest entry, type:

```bash
journalctl
```

By default, this will show you entries from the current and previous boots if `journald` is configured to save previous boot records. Some distributions enable this by default, while others do not (to enable this, either edit the `/etc/systemd/journald.conf` file and set the `Storage=` option to “persistent”, or create the persistent directory by typing `sudo mkdir -p /var/log/journal`).

If you only wish to see the journal entries from the current boot, add the `-b` flag:

```bash
journalct -b
```

To see only kernel messages, such as those that are typically represented by `dmesg`, you can use the `-k` flag:

```bash
journalctl -k
```

Again, you can limit this only to the current boot by appending the `-b` flag:

```bash
journalctl -k -b
```

## Querying Unit States and Logs

While the above commands gave you access to the general system state, you can also get information about the state of individual units.

To see an overview of the current state of a unit, you can use the `status` option with the `systemctl` command. This will show you whether the unit is active, information about the process, and the latest journal entries:

```bash
systemctl status httpd.service
```

To see all of the journal entries for the unit in question, give the `-u` option with the unit name to the `journalctl` command:

```bash
journalctl -u httpd.service
```

As always, you can limit the entries to the current boot by adding the `-b` flag:

```bash
journalctl -b -u httpd.service
```

Following logs (see new entries appear) u do with:

```bash
journalctl -feu httpd.service
```

## Inspecting Units and Unit Files

By now, you know how to modify a unit’s state by starting or stopping it, and you know how to view state and journal information to get an idea of what is happening with the process. However, we haven’t seen yet how to inspect other aspects of units and unit files.

A unit file contains the parameters that `systemd` uses to manage and run a unit. To see the full contents of a unit file, type:

```bash
systemctl cat httpd.service
```

To see the dependency tree of a unit (which units `systemd` will attempt to activate when starting the unit), type:

```bash
systemctl list-dependencies httpd.service
```

Finally, to see the low-level details of the unit’s settings on the system, you can use the `show` option:

```bash
systemctl show httpd.service
```

This will give you the value of each parameter being managed by `systemd`.

## Modifying Unit Files

If you need to make a modification to a unit file, `systemd` allows you to make changes from the `systemctl` command itself so that you don’t have to go to the actual disk location.

To add a unit file snippet, which can be used to append or override settings in the default unit file, simply call the `edit` option on the unit:

```bash
sudo systemctl edit httpd.service
```

After modifying a unit file, you should reload the `systemd` process itself to pick up your changes:

```bash
sudo systemctl daemon-reload
```

## Stopping or Rebooting the Server

For some of the major states that a system can transition to, shortcuts are available. For instance, to power off your server, you can type:

```bash
sudo systemctl poweroff
```

If you wish to reboot the system instead, that can be accomplished by typing:

```bash
sudo systemctl reboot
```

Note that most operating systems include traditional aliases to these operations so that you can simply type `sudo poweroff` or `sudo reboot` without the `systemctl`. However, this is not guaranteed to be set up on all systems

## Sources
- https://www.digitalocean.com/community/tutorials/systemd-essentials-working-with-services-units-and-the-journal
- https://www.linode.com/docs/guides/what-is-systemd/


