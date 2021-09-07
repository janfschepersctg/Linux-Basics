# Linux 
## Warming up
Try to find the hidden word in this exercise. 
Clone the repo in `srv01` and follow the instructions described in the README.

url: [click here](https://github.com/krother/bash_tutorial)

`aptenodytes patagonicus`

## Systemd
1) create a `sleep.service` (note: look up where service files are located)
`/lib/systemd/system`

```bash sleep.service 
[Unit]
Description=Sleep service
After=auditd.service systemd-user-sessions.service time-sync.target

[Service]
ExecStart=/usr/bin/sleep 10
Restart=on-success

[Install]
WantedBy=multi-user.target
```

2) enable the service
`systemctl enable sleep`
3) start the service
`systemctl start sleep`
4) check the status
`systemctl status sleep`
5) follow the logs of the service, confirm the service is restarting every 10 seconds
`journalctl -feu  sleep`
5) change the sleep parameter to 5 seconds. Confirm it is working while following the logs.
`systemctl daemon-reload
systemctl restart sleep
journalctl -feu sleep
`
6) stop and disable the service
`
systemctl stop sleep
systemctl disable sleep
`

## Permissions
-   Create a file `/tmp/empty.file` as the vagrant user and set the permissions to -r--r--r--
    `
    sudo -u vagrant touch /tmp/empty.file
    chmod 444 /tmp/empty.file
    `

-   Then set it to -rwx-------
    `
    chmod 700 /tmp/empty.file
    `
-   Create a second user `ctg`.
    `adduser ctg`
-   Change the file in `/tmp` so the ctg user can read but cannot write to it.
    `chmod 704 /tmp/empty.file `
-   convert the file to a bash script echoing "hello world". change the permissions the ctg user can only execute it, but not read it
    `this is not possible: the interpreter needs to read the script. only binaries you can make execute only`

## Process Control

- start a `sleep 100000000` process in the background
  `sleep 100000000 &`
- find all the pid's of the process
- kill the process

## Repository and package management

1) Clean all local repository and package (cache)data
`yum clean all`
2) update the system. 
`yum update`
3) Search if you can find the htop package.
`yum search htop`
4) install the `epel-release` package. This will install a repository file
`yum install epel-release`
5) find out where the epel.repo file is installed
`/etc/yum.repos.d/`
6) list all repos and verify epel is available
`yum repolist`
7) list all packages under the epel repository
`yum --disablerepo="*" --enablerepo="epel" list available`
8) Search if you can find the htop package.
`yum search htop`
9) give the summary of the htop package
`yum info htop`
10) install htop and run it with `htop`
`yum install -y htop`
11) remove htop from the system
`yum remove htop`

## Shell scripting exercise
answers: `https://medium.com/@sankad_19852/shell-scripting-exercises-5eb7220c2252`

1) Write a shell script that prints “Shell Scripting is Fun!” on the screen
2) Modify the shell script from exercise 1 to include a variable. The variable will hold the contents of the message “Shell Scripting is Fun!”
3) Store the output of the command “hostname” in a variable. Display “This script is running on _.” where “_” is the output of the “hostname” command.
4) Write a shell script to check to see if  "file_path" exists (use a variable). 
If it does exist, echo “the file exists.” Next, check to see if you can write to the file. If you can, display “You have permissions to edit “file_path.”
If you cannot find the file, display “You do NOT have permissions to edit “file_path””
5) rewrite the shell script above that prompts the user for the name of a file or directory.
6) Modify the previous script to that it accepts the file or directory name as an argument instead of prompting the user to enter it.
7) Modify the previous script to accept an unlimited number of files and directories as arguments.
8) Write a shell script that displays “man”,”bear”,”pig”,”dog”,”cat”,and “sheep” on the screen with each appearing on a separate line. Try to do this in as few lines as possible.
9) Write a shell script that displays, “This script will exit with 0 exit status.” Be sure that the script does indeed exit with a 0 exit status.
10) Write a shell script that accepts a file or directory name as an argument. Have the script report if it is reguler file, a directory, or another type of file. If it is a directory, exit with a 1 exit status. If it is some other type of file, exit with a 2 exit status.
11) Write a script that executes the command “cat/etc/shadow”. If the command return a 0 exit status, report “command succeeded” and exit with a 0 exit status. If the command returns a non-zero exit status, report “Command failed” and exit with a 1 exit status.
12) Write a shell script that consists of a function that displays the number of files in the present working directory. Name this function “file_count” and call it in your script. If you use variable in your function, remember to make it a local variable.
13) Write a shell script that exits on error and displays command as they will execute, including all expansions and substitutions. Use 3 ls command in your script. Make the first one succeed, the second one fail, and third one succeed. If you are using the proper options, the third ls command not be executed.
14) Modify the previous exercise so that script continuous, even if an error occurs. This time, all three ls command will execute.

## vim
1) install vim
2) run `vimtutor`  and follow the on screen introductions
