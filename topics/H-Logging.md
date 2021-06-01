# Logging
## introduction 
Linux logs give you a visual history of everything that’s been happening in the heart of a Linux operating system. So, if anything goes wrong, they give a useful overview of events in order to help you, the administrator, seek out the culprits.

For problems relating to particular apps, the developer decides where best to put the log of events. This can be cumbersome, but as administrator you'll have to figure out where this is.

Linux log files should be easy to decipher since they’re stored in text form under the /var/log directory and subdirectory. They cover all kinds of things, like system, kernel, package managers, MySQL and more. But now, we’ll focus on system logs.

## Log categories 

Most directories can be grouped under four headings:

-   Application Logs
-   Event Logs
-   Service Logs
-   System Logs

## Most common logfiles
-   **/var/log/syslog** or **/var/log/messages**: general messages, as well as system-related information. Essentially, this log stores all activity data across the global system. Note that activity for Redhat-based systems, such as CentOS or Rhel, are stored in messages, while Ubuntu and other Debian-based systems are stored in Syslog.
-   **/var/log/auth.log** or **/var/log/secure**: store authentication logs, including both successful and failed logins and authentication methods. Again, the system type dictates where authentication logs are stored; Debian/Ubuntu information is stored in /var/log/auth.log, while Redhat/CentrOS is stored in /var/log/secure.
-   **/var/log/boot.log**: a repository of all information related to booting and any messages logged during startup.
-   **/var/log/maillog or var/log/mail.log:** stores all logs related to mail servers, useful when you need information about postfix, smtpd, or any email-related services running on your server.
-   **/var/log/kern**: stores Kernel logs and warning data. This log is valuable for troubleshooting custom kernels as well.
-   **/var/log/dmesg**: messages relating to device drivers. The command **dmesg** can be used to view messages in this file.
-   **/var/log/faillog:** contains information all failed login attempts, which is useful for gaining insights on attempted security breaches, such as those attempting to hack login credentials as well as brute-force attacks.
-   **/var/log/cron**: stores all Crond-related messages (cron jobs), such as when the cron daemon initiated a job, related failure messages, etc.
-   **/var/log/yum.log:** if you install packages using the **yum** command, this log stores all related information, which can be useful in determining whether a package and all components were correctly installed.
-   **/var/log/httpd/**: a directory containing error_log and access_log files of the Apache httpd daemon. The **error_log** contains all errors encountered by httpd. These errors include memory issues and other system-related errors. **access_log** contains a record of all requests received over HTTP.
-   **/var/log/mysqld.log** or **/var/log/mysql.log** : MySQL log file that logs all debug, failure and success messages. Contains information about the starting, stopping and restarting of MySQL daemon mysqld. This is another instance where the system dictates the directory; RedHat, CentOS, Fedora, and other RedHat-based systems use /var/log/mysqld.log, while Debian/Ubuntu use the /var/log/mysql.log directory.

## How to use logs for debugging
### Searching with Grep

One of the simplest ways to analyze logs is by performing plain text searches using grep. grep is a command line tool that can search for matching text in a file, or in output from other commands.

To perform a simple search, enter your search string followed by the file you want to search. Here, we search the authentication log for lines containing “user hoover”.
```bash
$ grep "user hoover" /var/log/auth.log
pam_unix(sshd:session): session opened for user hoover by (uid=0)
pam_unix(sshd:session): session closed for user hoover
```
Note that this returns lines containing the _exact match_. This makes it useful for searches where you know exactly what you’re looking for.

You can also utilize grep to "surround search". Using surround search returns a number of lines before or after a match. This provides context for each event by letting you trace the events that led up to or immediately followed the event. The -B flag specifies how many lines to return before the event, and the -A flag specifies the number of lines after.
```bash
$ grep -B 3 -A 2 'Invalid user' /var/log/auth.log
Apr 28 17:06:20 ip-172-31-11-241 sshd[12545]: reverse mapping checking getaddrinfo for 216-19-2-8.commspeed.net [216.19.2.8] failed - POSSIBLE BREAK-IN ATTEMPT!
Apr 28 17:06:20 ip-172-31-11-241 sshd[12545]: Received disconnect from 216.19.2.8: 11: Bye Bye [preauth]
Apr 28 17:06:20 ip-172-31-11-241 sshd[12547]: Invalid user admin from 216.19.2.8
Apr 28 17:06:20 ip-172-31-11-241 sshd[12547]: input_userauth_request: invalid user admin [preauth]
Apr 28 17:06:20 ip-172-31-11-241 sshd[12547]: Received disconnect from 216.19.2.8: 11: Bye Bye [preauth]
```
### Tail

Tail is another command line tool that can display the latest changes from a file **in real time**. This is useful for monitoring ongoing processes, such as restarting a service or testing a code change. You can also use tail to print the last few lines of a file, or pair it with grep to filter the output from a log file.
```bash
$ tail -f /var/log/auth.log | grep 'Invalid user'
Apr 30 19:49:48 ip-172-31-11-241 sshd[6512]: Invalid user ubnt from 219.140.64.136
Apr 30 19:49:49 ip-172-31-11-241 sshd[6514]: Invalid user admin from 219.140.64.136
```
For following systemd logging in real time, u can use
```bash
journalctl -feu $name.service
```
### Less
 Less is a command line utility that displays the contents of a file or a command output, one page at a time. It is similar to `more`, but has more advanced features and allows you to navigate both forward and backward through the file.

When starting `less` doesn’t read the entire file which results in much faster load times compared to text editors like `vim`.

The general syntax for the `less` program is as follows:

```bash
less [OPTIONS] filename
```

You can also redirect the output from a command to `less` using a pipe. For example, to view the output of the `ps` command page by page you would type:
```
ps aux | less
```
When opening a file which content is too large to fit in one page, you will see a single colon (`:`).

To go forward to the next page press either the `f` key or `Space bar`. If you want to move down for a specific number of lines, type the number followed by the space or `f` key.

You can press either the `Down arrow` or `Enter` to scroll forward by one line and `Up arrow` scroll backward by one line.

To go back to the previous page hit the `b` key. Move up for a specific number of lines, by typing the number followed by the `b` key.

If you want to search for a pattern, type forward slash (`/`) followed by the pattern you want to search. Once you hit `Enter` less will search forward for matches. To search backwards use (`?`) followed by the search pattern.

When the end of the file is reached, the string `(END)` is shown at the bottom of the screen.

To quit `less` and go back to the command line press `q`


## Sources
- https://www.plesk.com/blog/featured/linux-logs-explained/
- https://stackify.com/linux-logs/
- https://www.loggly.com/ultimate-guide/analyzing-linux-logs/
- https://linuxize.com/post/less-command-in-linux/

