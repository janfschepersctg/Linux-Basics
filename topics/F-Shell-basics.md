# Shell basics

## What Is a Shell?

You use a Linux shell program to interact with your system by typing commands (the _input stream_) at a terminal and seeing output (the _output stream_) and error messages (the _error stream_) on the same terminal. Sometimes you need to run commands before the system has booted far enough to allow terminal connections, and sometimes you need to run commands periodically, whether you are logged in. A shell can do these tasks for you, too. The standard input and output streams do not have to come from, or be directed to, a real user at a terminal. In this guide, you learn more about shells and customizing the user’s environment. In particular, you learn about the bash (Bourne again) shell — an enhancement of the original Bourne shell.

## Shells and environments

A shell provides a layer between you and the intricacies of an operating system. With Linux (and UNIX) shells, you can build complex operations by combining basic functions. Using programming constructs, you can then build functions for direct execution in the shell or save functions as _shell scripts_. A shell script is a sequence of commands that is stored in a file that the shell can run as needed.

When you are running a bash shell, you have a _shell environment_. The environment is a set of name-value pairs that define the form of your prompt, your home directory, your working directory, the name of your shell, files that you have opened, functions that you have defined, and more. The environment is available to every shell process. When a shell starts, it assigns values from the environment to _shell variables_. You can use shells, including bash, to create and modify additional shell variables. You can then export such variables to be part of the environment that is inherited by child processes that you spawn from your current shell.

## How the Environment and Environmental Variables Work

Every time a shell session spawns, a process takes place to gather and compile information that should be available to the shell process and its child processes. It obtains the data for these settings from a variety of different files and settings on the system.

The environment provides a medium through which the shell process can get or set settings and, in turn, pass these on to its child processes.

The environment is implemented as strings that represent key-value pairs. If multiple values are passed, they are typically separated by colon (`:`) characters. Each pair will generally look something like this:

```
KEY=value1:value2:...
```

If the value contains significant white-space, quotations are used:

```
KEY="value with spaces"
```

The keys in these scenarios are variables. They can be one of two types, environmental variables or shell variables.

**Environmental variables** are variables that are defined for the current shell and are inherited by any child shells or processes. Environmental variables are used to pass information into processes that are spawned from the shell.

**Shell variables** are variables that are contained exclusively within the shell in which they were set or defined. They are often used to keep track of ephemeral data, like the current working directory.

By convention, these types of variables are usually defined using all capital letters. This helps users distinguish environmental variables within other contexts.

Each shell session keeps track of its own shell and environmental variables. We can access these in a few different ways.

We can see a list of all of our environmental variables by using the `env` or `printenv` commands. In their default state, they should function exactly the same:

```bash
$ env
SHELL=/bin/bash
TERM=xterm
USER=demouser
LS_COLORS=rs=0:di=01;34:ln=01;36:mh=00:pi=40;33:so=01;35:do=01;35:bd=40;33;01:cd=40;33;01:or=40;31;01:su=37;41:sg=30;43:ca:...
MAIL=/var/mail/demouser
PATH=/usr/local/bin:/usr/bin:/bin:/usr/local/games:/usr/games
PWD=/home/demouser
LANG=en_US.UTF-8
SHLVL=1
HOME=/home/demouser
LOGNAME=demouser
LESSOPEN=| /usr/bin/lesspipe %s
LESSCLOSE=/usr/bin/lesspipe %s %s
_=/usr/bin/printenv
```
`env` lets you modify the environment that programs run in by passing a set of variable definitions into a command like this:

```bash 
env VAR1="value" command_to_run command_options
```
Since, as we learned above, child processes typically inherit the environmental variables of the parent process, this gives you the opportunity to override values or add additional variables for the child.

### Common Environmental  Variables

Some environmental and shell variables are very useful and are referenced fairly often.  
Here are some common environmental variables that you will come across:

-   `SHELL`: This describes the shell that will be interpreting any commands you type in. In most cases, this will be bash by default, but other values can be set if you prefer other options.
-   `TERM`: This specifies the type of terminal to emulate when running the shell. Different hardware terminals can be emulated for different operating requirements. You usually won’t need to worry about this though.
-   `USER`: The current logged in user.
-   `PWD`: The current working directory.
-   `OLDPWD`: The previous working directory. This is kept by the shell in order to switch back to your previous directory by running `cd -`.
-   `LS_COLORS`: This defines color codes that are used to optionally add colored output to the `ls` command. This is used to distinguish different file types and provide more info to the user at a glance.
-   `MAIL`: The path to the current user’s mailbox.
-   `PATH`: A list of directories that the system will check when looking for commands. When a user types in a command, the system will check directories in this order for the executable.
-   `LANG`: The current language and localization settings, including character encoding.
-   `HOME`: The current user’s home directory.
-   `_`: The most recent previously executed command.

### Creating Shell Variables

We will begin by defining a shell variable within our current session. This is easy to accomplish; we only need to specify a name and a value. We’ll adhere to the convention of keeping all caps for the variable name, and set it to a simple string.

```bash
TEST_VAR='Hello World!'
```

Here, we’ve used quotations since the value of our variable contains a space. Furthermore, we’ve used single quotes because the exclamation point is a special character in the bash shell that normally expands to the bash history if it is not escaped or put into single quotes.

We now have a shell variable. This variable is available in our current session, but will not be passed down to child processes.

### Creating Environmental Variables

Now, let’s turn our shell variable into an environmental variable. We can do this by _exporting_ the variable. The command to do so is appropriately named:

```bash
export TEST_VAR
```
## Unsetting Variables

If we want to completely unset a variable, either shell or environmental, we can do so with the `unset` command:
```bash
unset TEST_VAR
```
## Setting Environmental Variables at Login

We’ve already mentioned that many programs use environmental variables to decide the specifics of how to operate. We do not want to have to set important variables up every time we start a new shell session, and we have already seen how many variables are already set upon login, so how do we make and define variables automatically?

This is actually a more complex problem than it initially seems, due to the numerous configuration files that the bash shell reads depending on how it is started.

### The Difference between Login, Non-Login, Interactive, and Non-Interactive Shell Sessions

The bash shell reads different configuration files depending on how the session is started.

One distinction between different sessions is whether the shell is being spawned as a **login** or **non-login** session.

A **login** shell is a shell session that begins by authenticating the user. If you are signing into a terminal session or through SSH and authenticate, your shell session will be set as a login shell.

If you start a new shell session from within your authenticated session, like we did by calling the `bash` command from the terminal, a **non-login** shell session is started. You were were not asked for your authentication details when you started your child shell.

Another distinction that can be made is whether a shell session is interactive, or non-interactive.

An **interactive** shell session is a shell session that is attached to a terminal. A **non-interactive** shell session is one is not attached to a terminal session.

So each shell session is classified as either login or non-login and interactive or non-interactive.

A normal session that begins with SSH is usually an interactive login shell. A script run from the command line is usually run in a non-interactive, non-login shell. A terminal session can be any combination of these two properties.

Whether a shell session is classified as a login or non-login shell has implications on which files are read to initialize the shell session.

A session started as a login session will read configuration details from the `/etc/profile` file first. It will then look for the first login shell configuration file in the user’s home directory to get user-specific configuration details.

It reads the first file that it can find out of `~/.bash_profile`, `~/.bash_login`, and `~/.profile` and does not read any further files.

In contrast, a session defined as a non-login shell will read `/etc/bash.bashrc` and then the user-specific `~/.bashrc` file to build its environment.

Non-interactive shells read the environmental variable called `BASH_ENV` and read the file specified to define the new environment.

### Implementing Environmental Variables

As you can see, there are a variety of different files that we would usually need to look at for placing our settings.

This provides a lot of flexibility that can help in specific situations where we want certain settings in a login shell, and other settings in a non-login shell. However, most of the time we will want the same settings in both situations.

Fortunately, most Linux distributions configure the login configuration files to source the non-login configuration files. This means that you can define environmental variables that you want in both inside the non-login configuration files. They will then be read in both scenarios.

We will usually be setting user-specific environmental variables, and we usually will want our settings to be available in both login and non-login shells. This means that the place to define these variables is in the `~/.bashrc` file.

Open this file now:

```bash
vim ~/.bashrc
```

This will most likely contain quite a bit of data already. Most of the definitions here are for setting bash options, which are unrelated to environmental variables. You can set environmental variables just like you would from the command line:

```bash
export VARNAME=value
```

Any new environmental variables can be added anywhere in the `~/.bashrc` file, as long as they aren’t placed in the middle of another command or for loop. We can then save and close the file. The next time you start a shell session, your environmental variable declaration will be read and passed on to the shell environment. You can force your current session to read the file now by typing:

```bash
source ~/.bashrc
```

If you need to set system-wide variables, you may want to think about adding them to `/etc/profile`, `/etc/bash.bashrc`, or `/etc/environment`.

## Sources 
https://developer.ibm.com/technologies/linux/tutorials/l-lpic1-105-1/
https://www.digitalocean.com/community/tutorials/how-to-read-and-set-environmental-and-shell-variables-on-linux

