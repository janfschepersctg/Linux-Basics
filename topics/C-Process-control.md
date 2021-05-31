# Process control
## Introduction
A process is the abstraction used by UNIX to represent a running program. It is the object through which a program’s use of memory, processor time, and I/O resources can be managed and monitored.

It is part of the UNIX philosophy that as much work as possible be done within the context of processes, rather than handled specially by the kernel. Although portions of the kernel cannot be made to fit this model, it is used by most system software. System and user processes all follow the same rules so that you can use a single set of tools to control them both

### Components of a process 
A process consists of an address space and a set of data structures with the kernel. The address space is a set of memory pages that the kernel has marked for the process’s use. It contains the code and libraries that the process is executing, the process’s variables, its stacks, and various extra information needed by the kernel while the process is running. Since UNIX supports virtual memory, there is not necessarily a correlation between a page’s location within an address space and its location inside the machine’s physical memory or swap space.

The kernel’s internal data structures record various pieces of information about each process. Some of the more important data structures are:
- The process’s address space map
- The current status of the process, e.g. sleeping, stopped, runnable, zombie, etc
- The execution priority of the process
- Information about the resources the process has used
- The process’s signal mask, a record of which signals are blocked
- The owner of the process

Many of the parameters associated with a process directly affect its execution: the amount of processor time it gets, the files it can access, etc.

### PID: Process ID Number
The kernel assigns a unique ID number to every process. Most commands and system calls that manipulate processes require you to specify a PID to identify the target of the operation. PIDs are assigned in order as processes are created. When the kernel run outof PIDs, it starts again at 1, skipping over any PIDs that are still in use.

### PPID : Parent PID
UNIX does not supply a system call that creates a new process running a particular program. Instead an existing process must clone itself to create a new process. The clone can then exchange the program it is running for a different one.

When a process’s UID is the user identification number of the person who created it, or more accurately, it is a copy of the EUID value of the parent process. Usually only the creator, aka the owner, and the superuserare permitted to manipulate a process. The EUID, is the “effective” user ID, an extra UID used to determine what resources and files a process has permission to access at any given moment. For most processes the UID and EUID are the same, the usual exception being programs that are set-uid

### GID and EGID: Real and Effective Group ID
GID and EGID: Real and Effective Group IDThe GID is the group identification number of a process. The EGID is related to the GID in the same manner that the EUID is related to the UID. If a process tries to access a file for which it does not have owner permission, the kernel will automatically check to see if permission may be granted on the basis of the EGID.

### Summary

   - **pid**: The is the process ID (PID) of the process you call the Process.pid method in.
   - **ppid**: The PID of the parent process (the process that spawned the current one). For example, if you run ruby test.rb in a bash shell, PPID in that process would be the PID of Bash.
   - **uid**: The UNIX ID of the user the process is running under.
   - **euid**: The effective user ID that the process is running under. The EUID determines what a program is allowed to do, based on what the user with this UID is allowed to do. Typically the same as uid, but can be different with commands like sudo.
   - **gid**: The UNIX group ID the program is running under.
   - **egid**: Like euid, but for groups.

## Working with processes
### Keeping a process running

A process may not continue to run when you log out or close your terminal. This special case can be avoided by preceding the command you want to run with the nohup command. Also, appending an ampersand (&) will send the process to the background and allow you to continue using the terminal. For example, suppose you want to run `myprogram.sh`.

`nohup myprogram.sh &`

One nice thing nohup does is return the running process's PID. I'll talk more about the PID next.

### Manage a running process

There are several commands that can check the status of a running process. Let's take a quick look at these.

#### PS

The most common is ps. The default output of ps is a simple list of the processes running in your current terminal. As you can see below, the first column contains the PID.

    $ ps  
    PID TTY          TIME CMD  
    23989 pts/0    00:00:00 bash  
    24148 pts/0    00:00:00 ps

If i would like to view a Nginx process for example, I tell ps to show me every running process (**-e**) and a full listing (**-f**).

    $ ps -ef  
    UID        PID  PPID  C STIME TTY          TIME CMD   
    root         1     0  0 Aug18 ?        00:00:10 /sbin/init splash  
    root         2     0  0 Aug18 ?        00:00:00 [kthreadd]  
    root         4     2  0 Aug18 ?        00:00:00 [kworker/0:0H]  
    root         6     2  0 Aug18 ?        00:00:00 [mm_percpu_wq]  
    root         7     2  0 Aug18 ?        00:00:00 [ksoftirqd/0]  
    root         8     2  0 Aug18 ?        00:00:20 [rcu_sched]  
    root         9     2  0 Aug18 ?        00:00:00 [rcu_bh]  
    root        10     2  0 Aug18 ?        00:00:00 [migration/0]  
    root        11     2  0 Aug18 ?        00:00:00 [watchdog/0]  
    root        12     2  0 Aug18 ?        00:00:00 [cpuhp/0]  
    root        13     2  0 Aug18 ?        00:00:00 [cpuhp/1]  
    root        14     2  0 Aug18 ?        00:00:00 [watchdog/1]  
    root        15     2  0 Aug18 ?        00:00:00 [migration/1]  
    root        16     2  0 Aug18 ?        00:00:00 [ksoftirqd/1]  
    alan     20506 20496  0 10:39 pts/0    00:00:00 bash  
    alan     20520  1454  0 10:39 ?        00:00:00 nginx: master process nginx  
    alan     20521 20520  0 10:39 ?        00:00:00 nginx: worker process  
    alan     20526 20506  0 10:39 pts/0    00:00:00 man ps  
    alan     20536 20526  0 10:39 pts/0    00:00:00 pager  
    alan     20564 20496  0 10:40 pts/1    00:00:00 bash

You can see the Nginx processes in the output of the ps command above. The command displayed almost 300 lines, but I shortened it for this illustration. As you can imagine, trying to handle 300 lines of process information is a bit messy. We can pipe this output to grep to filter out nginx.

    $ ps -ef |grep nginx  
    alan     20520  1454  0 10:39 ?        00:00:00 nginx: master process nginx  
    alan     20521 20520  0 10:39 ?        00:00:00 nginx: worker process

That's better. We can quickly see that Nginx has PIDs of 20520 and 20521.

#### PGREP

The pgrep command was created to further simplify things by removing the need to call grep separately.

    $ pgrep nginx  
    20520  
    20521

Suppose you are in a hosting environment where multiple users are running several different instances of Nginx. You can exclude others from the output with the **-u** option.

    $ pgrep -u alan nginx  
    20520  
    20521

#### PIDOF

Another nifty one is pidof. This command will check the PID of a specific binary even if another process with the same name is running. To set up an example, I copied a Nginx to a second directory and started it with the prefix set accordingly. In real life, this instance could be in a different location, such as a directory owned by a different user. If I run both Nginx instances, the **ps -ef** output shows all their processes.

    ps -ef |grep nginx  
    alan     20881  1454  0 11:18 ?        00:00:00 nginx: master process ./nginx -p /home/alan/web/prod/nginxsec  
    alan     20882 20881  0 11:18 ?        00:00:00 nginx: worker process  
    alan     20895  1454  0 11:19 ?        00:00:00 nginx: master process nginx  
    alan     20896 20895  0 11:19 ?        00:00:00 nginx: worker process

Using grep or pgrep will show PID numbers, but we may not be able to discern which instance is which.

    $ pgrep nginx  
    20881  
    20882  
    20895  
    20896

The pidof command can be used to determine the PID of each specific Nginx instance.

    $ pidof /home/alan/web/prod/nginxsec/sbin/nginx  
    20882 20881  
    $ pidof /home/alan/web/prod/nginx/sbin/nginx  
    20896 20895

#### TOP

The top command has been around a long time and is very useful for viewing details of running processes and quickly identifying issues such as memory hogs. Its default view is shown below.

    top - 11:56:28 up 1 day, 13:37,  1 user,  load average: 0.09, 0.04, 0.03  
    Tasks: 292 total,   3 running, 225 sleeping,   0 stopped,   0 zombie  
    %Cpu(s):  0.1 us,  0.2 sy,  0.0 ni, 99.7 id,  0.0 wa,  0.0 hi,  0.0 si,  0.0 st  
    KiB Mem : 16387132 total, 10854648 free,  1859036 used,  3673448 buff/cache  
    KiB Swap:        0 total,        0 free,        0 used. 14176540 avail Mem   
      
      PID USER      PR  NI    VIRT    RES    SHR S  %CPU %MEM     TIME+ COMMAND  
    17270 alan      20   0 3930764 247288  98992 R   0.7  1.5   5:58.22 gnome-shell  
    20496 alan      20   0  816144  45416  29844 S   0.5  0.3   0:22.16 gnome-terminal-  
    21110 alan      20   0   41940   3988   3188 R   0.1  0.0   0:00.17 top  
        1 root      20   0  225564   9416   6768 S   0.0  0.1   0:10.72 systemd  
        2 root      20   0       0      0      0 S   0.0  0.0   0:00.01 kthreadd  
        4 root       0 -20       0      0      0 I   0.0  0.0   0:00.00 kworker/0:0H  
        6 root       0 -20       0      0      0 I   0.0  0.0   0:00.00 mm_percpu_wq  
        7 root      20   0       0      0      0 S   0.0  0.0   0:00.08 ksoftirqd/0

The update interval can be changed by typing the letter **s** followed by the number of seconds you prefer for updates. To make it easier to monitor our example Nginx processes, we can call top and pass the PID(s) using the **-p** option. This output is much cleaner.

    $ top -p20881 -p20882 -p20895 -p20896  
      
    Tasks:   4 total,   0 running,   4 sleeping,   0 stopped,   0 zombie  
    %Cpu(s):  2.8 us,  1.3 sy,  0.0 ni, 95.9 id,  0.0 wa,  0.0 hi,  0.0 si,  0.0 st  
    KiB Mem : 16387132 total, 10856008 free,  1857648 used,  3673476 buff/cache  
    KiB Swap:        0 total,        0 free,        0 used. 14177928 avail Mem   
      
      PID USER      PR  NI    VIRT    RES    SHR S  %CPU %MEM     TIME+ COMMAND  
    20881 alan      20   0   12016    348      0 S   0.0  0.0   0:00.00 nginx  
    20882 alan      20   0   12460   1644    932 S   0.0  0.0   0:00.00 nginx  
    20895 alan      20   0   12016    352      0 S   0.0  0.0   0:00.00 nginx  
    20896 alan      20   0   12460   1628    912 S   0.0  0.0   0:00.00 nginx

It is important to correctly determine the PID when managing processes, particularly stopping one. Also, if using top in this manner, any time one of these processes is stopped or a new one is started, top will need to be informed of the new ones.

### Stopping a process

#### KILL

Interestingly, there is no stop command. In Linux, there is the kill command. Kill is used to send a signal to a process. The most commonly used signal is "terminate" (SIGTERM) or "kill" (SIGKILL). However, there are many more. Below are some examples. The full list can be shown with **kill -L**.

     1) SIGHUP       2) SIGINT       3) SIGQUIT      4) SIGILL       5) SIGTRAP  
     6) SIGABRT      7) SIGBUS       8) SIGFPE       9) SIGKILL     10) SIGUSR1  
    11) SIGSEGV     12) SIGUSR2     13) SIGPIPE     14) SIGALRM     15) SIGTERM

Notice signal number nine is SIGKILL. Usually, we issue a command such as **kill -9 20896**. The default signal is 15, which is SIGTERM. Keep in mind that many applications have their own method for stopping. Nginx uses a **-s** option for passing a signal such as "stop" or "reload." Generally, I prefer to use systemctl to stop an operation. However, I'll demonstrate the kill command to stop Nginx process 20896 and then confirm it is stopped with pgrep. The PID 20896 no longer appears.

    $ kill -9 20896  
       
    $ pgrep nginx  
    20881  
    20882  
    20895  
    22123

#### PKILL

The command pkill is similar to pgrep in that it can search by name. This means you have to be very careful when using pkill. In my example with Nginx, I might not choose to use it if I only want to kill one Nginx instance. 

## Sources
- https://www.cs.clemson.edu/course/cpsc424/material/Processes/Components.pdf
- https://stackoverflow.com/questions/30493424/what-is-the-difference-between-a-process-pid-ppid-uid-euid-gid-and-egid/30493537
- https://opensource.com/article/18/9/linux-commands-process-management

