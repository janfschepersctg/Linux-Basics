# Basic navigation

### pwd

`pwd` (print working directory) shows the current _directory_ (basically, the folder) you’re in.

In case you’re wondering:
```
$ pwd
/home/brillydev/workspace/foo/bar

$ cd ..
$ pwd
/home/brillydev/workspace/foo
```

-   `~` (tilde) means the user’s home directory, usually /home/username

-   `.` (dot) means the current directory you’re in

-   `..` (dot dot) means the parent directory of the current directory you’re in.
    
    For example, if you’re in `foo/bar/`, `.` will represent `bar/`, `..` will represent `foo/`.
    

### cd

The most basic command of all time, `cd` (change directory) means... Err, change directory.

```
$ pwd
/home/brillydev/workspace/foo/bar

$ cd ..
$ pwd
/home/brillydev/workspace/foo
```

You can see that the directory changes according to what you type after `cd`. Typing `cd` alone without any _argument_ (without anything that follows it) will bring you to the home directory of the user.

`cd` followed by a dash (`-`)will bring you to the recent directory you were in.

```
$ cd
$ pwd
/home/brillydev

$ cd workspace/foo
$ pwd
/home/brillydev/workspace/foo

$ cd -
$ pwd
/home/brillydev
```

### ls

`ls` (list) list down all the content inside the directory.

```
$ pwd
/home/brillydev/workspace

$ ls
apple.txt bar/ foo/ somefiles.txt
```

A slash (`/`) post-fixed after a name indicates that it is a directory. In this case, `bar` and `foo` are directories. Anything not with a slash are all files.

### Flags

In addition to performing a general task, a command may also contain flags to specify a specific task you want the command to do. A flag is anything prefixed with a dash (`-`) that follows the command name.

For example, you can type `ls -l`. In this case, `l` being the flag, to display the content of the directory in a nice list view.
```
$ ls -l
total 8
-rw-r--r-- 1 brillydev brillydev 0 Oct 22 13:18 apple.txt
drwxr-xr-x 2 brillydev brillydev 4096 Jan 31 03:55 bar/
drwxr-xr-x 2 brillydev brillydev 4096 Oct 22 13:18 foo/
-rw-r--r-- 1 brillydev brillydev 0 Feb 6 14:08 somefiles.txt
```
Flags can also be combined. `ls -a` display all content, including hidden files (files that are prefixed with a dot). When used with `ls -l`, we can combine them like this:

```
$ ls -la
total 16
drwxr-xr-x 4 brillydev brillydev 4096 Feb 21 08:04 ./
drwxr-xr-x 10 brillydev brillydev 4096 Feb 21 07:55 ../
-rw-r--r-- 1 brillydev brillydev 0 Oct 22 13:18 .hiddenfile.txt
-rw-r--r-- 1 brillydev brillydev 0 Oct 22 13:18 apple.txt
drwxr-xr-x 2 brillydev brillydev 4096 Jan 31 03:55 bar/
drwxr-xr-x 2 brillydev brillydev 4096 Oct 22 13:18 foo/
-rw-r--r-- 1 brillydev brillydev 0 Feb 6 14:08 somefiles.txt
```

Some flags can also be more than one-letter long. Those that are multiple letters long can be written with double dashes in front. For instance, `ls -a` can also be written as:

```
$ ls --all
./ ../ .hiddenfile.txt apple.txt bar/ foo/ somefiles.txt
```

### tree

For those who want more fancy visualization, `tree` is for you.

```
$ tree
.
├── apple.txt
├── bar
├── foo
└── somefiles.txt
2 directories, 2 files
```

### clear / reset / Ctrl + L / ⌘ + K

You’re having fun playing around with all these commands when you realize you screen is really cluttered and you need some clean up. Typing `clear` or `reset` or input any of the key combinations mentioned will get your terminal wiped up.

### File Execution

Surprisingly not many beginners know how to run a standalone binary/executable file. To execute a local file, simply type

```
$ ./filename
```

If you ever find yourself stuck in the program, simply press `Ctrl` + `C` to get out.

## Sources
https://www.pluralsight.com/guides/beginner-linux-navigation-manual
