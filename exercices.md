# Linux 
## Warming up
Try to find the hidden word in this exercise. 
Clone the repo in `srv01` and follow the instructions described in the README.

url: `https://github.com/krother/bash_tutorial`

## Systemd
1) create a `sleep.service` (note: look up where service files are located)
 
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
3) start the service
4) check the status
5) follow the logs of the service, confirm the service is restarting every 10 seconds
5) change the sleep parameter to 5 seconds. Confirm it is working while following the logs.
6) stop and disable the service

## Permissions
-   Create a file `empty.file` as the vagrant user and set the permissions to -r--r--r--
-   Then set it to -rwx-------
-   Create a second user `ctg`.
-   Create a file by vagrant in `/tmp` and make sure no other user can see the content.
-   Create another file in `/tmp` that the user can read but cannot write to.
-   Create a `echo "Hello World" shell script. Make sure both users can run it but only vagrant can write it.
-   Change the permission of the shell script only vagrant can run the shell script again.

## Process Control

- start a `sleep 100000000` process in the background
- use `top` to 
- find all the pid`s of the process
- kill the process

## File manipulation

1.  Change the present working directory to your personal directory
    
2.  Create a new directory called `ctg`
    
3.  Change the present working directory to the `ctg` directory
    
4.  Create two new directories called `labs` and `exercises`
    
5.  Remove all access permissions of `others` from the `exercises` directory
    
6.  Set `groups` to have read and execute permissions on the `exercises` directory
    
7.  Change the present working directory to `$HOME/ctg/labs`
    
8.  Create multiple empty files (and list them) using wildcards. Note: use the syntax `{1..5}` in combination with `touch` It is taken by the Linux shell as a series of sequential integers from `1` to `5`.
    
9.  Remove multiple files using wildcards. Note the syntax `*`. It is taken as “any characters” by the Linux shell.

## Repository and package management

1) Clean all local repository and package (cache)data
2) update the system. 
3) Search if you can find the htop package.
4) install the `epel-release` package. This will install a repository file
5) find out where the epel.repo file is installed
6) list all repos and verify epel is available
7) list all packages under the epel repository
8) Search if you can find the htop package.
9) give the summary of the htop package
10) install htop and run it with `htop`
11) remove htop from the system

## Shell scripting exercise

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
