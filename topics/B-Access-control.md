# ACCESS CONTROL
## General principles of access control
- access control depends on which user or group is attempting to perform and operation
- Objects (files and processes) have owners
- Objects are owned by the users creating them by default
- the "root" user is like superman, he can act as the owner of each object
- only root can perform certain sensitive administrative operation
 
## Filesystem access control
- Every file has an owner and group
- Both the kernel and filesystem track owners and groups as numbers (UID). These numbers are mapped to usernames in `/etc/passwd` and `/etc/group`

### Permission types
Each file or directory has three basic permission types:

-   **read (r)** – The Read permission refers to a user’s capability to read the contents of the file.
-   **write (w)** – The Write permissions refer to a user’s capability to write or modify a file or directory.
-   **execute (x)** – The Execute permission affects a user’s capability to execute a file or view the contents of a directory.

### Viewing the Permissions

You can view the permissions by checking the file or directory permissions with the `ls -l` command.

The permission in the command line is displayed as: _**_rwxrwxrwx 1 owner:group**_

1.  User rights/Permissions
    1.  The first character that I marked with an underscore is the special permission flag that can vary.
    2.  The following set of three characters (rwx) is for the owner permissions **(U)**.
    3.  The second set of three characters (rwx) is for the Group permissions **(G)**.
    4.  The third set of three characters (rwx) is for the All Users permissions **(O)**.
2.  Following that grouping since the integer/number displays the number of hard links to the file.
3.  The last piece is the Owner and Group assignment formatted as Owner:Group.

### Changing the permissions
The potential Assignment Operators are + (plus) and – (minus); these are used to tell the system whether to add or remove the specific permissions.

So for an example, lets say I have a file named file1 that currently has the permissions set to **_rw_rw_rw,** which means that the owner, group and all users have read and write permission. Now we want to remove the read and write permissions from the all users group.

To make this modification you would invoke the command: `chmod a-rw file1`  
To add the permissions above you would invoke the command: `chmod a+rw file1`

As you can see, if you want to grant those permissions you would change the minus character to a plus to add those permissions.

### Using binary references to set permissions
Now that you understand the permissions groups and types this one should feel natural. To set the permission using binary references you must first understand that the input is done by entering three integers/numbers.

A sample permission string would be `chmod 640 file1`, which means that the owner has read and write permissions, the group has read permissions, and all other user have no rights to the file.

The first number represents the Owner permission; the second represents the Group permissions; and the last number represents the permissions for all other users. The numbers are a binary representation of the rwx string.

-   __**r** = 4__
-   __**w** = 2__
-   __**x** = 1__

You add the numbers to get the integer/number representing the permissions you wish to set. You will need to include the binary permissions for each of the three permission groups.

So to set a file to permissions on file1 to read **__rwxr______**, you would enter `chmod 740 file1`.

### Owners and Groups
You use the chown command to change owner and group assignments, the syntax is simple `chown owner:group filename` so to change the owner of file1 to user1 and the group to family you would enter `chown user1:family file1`

## The root account
Linux `sudo` command is used to give `root` privileges to the normal users . `/etc/sudoers` file is used for configuration of `sudo` .  The Sudoers file provides the users who can run `sudo` command. Sudoers also used to limit the commands the user can run.

## 	The sudoers file
Sudoers file is the database which is used by `sudo` command. All specified rules are applied during 
`sudo` usage. 

For a detailed guide how to modify the sudoers file: https://www.garron.me/en/linux/visudo-command-sudoers-file-sudo-default-editor.html

## Examples of sudo
- run a restricted command: 
  `sudo yum install httpd`
- run the last command as sudo
   `sudo !!`
- run a command as another user 
   `sudo -u foo whoami`
 - switch to the root user
   `sudo -i` or `su - root`
   

## Sources
- https://phoenixnap.com/kb/linux-sudo-command
- https://www.poftut.com/linux-sudo-command-tutorial-with-examples-to-get-root-privileges/
- https://www.linux.com/training-tutorials/understanding-linux-file-permissions/
- Unix and linux system administration handbook
