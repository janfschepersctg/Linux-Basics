# Pipe

## Introduction
Every program we run on the command line automatically has three data streams connected to it.

-   STDIN (0) - Standard input (data fed into the program)
-   STDOUT (1) - Standard output (data printed by the program, defaults to the terminal)
-   STDERR (2) - Standard error (for error messages, also defaults to the terminal)

Piping and redirection is the means by which we may connect these streams between programs and files to direct data in interesting and useful ways.

We'll demonstrate piping and redirection below with several examples but these mechanisms will work with every program on the command line, not just the ones we have used in the examples.

## Redirecting to a File

Normally, we will get our output on the screen, which is convenient most of the time, but sometimes we may wish to save it into a file to keep as a record, feed into another system, or send to someone else. The greater than operator ( > ) indicates to the command line that we wish the programs output (or whatever it sends to STDOUT) to be saved in a file instead of printed to the screen. Let's see an example.
```bash
1.  $ ls
2.  barry.txt bob example.png firstfile foo1 video.mpeg
3.  $ ls > myoutput
4.  $ ls
5.  barry.txt bob example.png firstfile foo1 myoutput video.mpeg
6.  $ cat myoutput
7.  barry.txt
8.  bob
9.  example.png
10.  firstfile
11.  foo1
12.  myoutput
13.  video.mpeg
```

Let's break it down:

-   **Line 1** Let's start off by seeing what's in our current directory.
-   **Line 3** Now we'll run the same command but this time we use the > to tell the terminal to save the output into the file myoutput. You'll notice that we don't need to create the file before saving to it. The terminal will create it automatically if it does not exist.
-   **Line 4** As you can see, our new file has been created.
-   **Line 6** Let's have a look at what was saved in there.
### Saving to an Existing File

If we redirect to a file which does not exist, it will be created automatically for us. If we save into a file which already exists, however, then it's contents will be cleared, then the new output saved to it.
```bash
1.  $ cat myoutput
2.  barry.txt
3.  bob
4.  example.png
5.  firstfile
6.  foo1
7.  myoutput
8.  video.mpeg
9.  $ wc -l barry.txt > myoutput
10. $ cat myoutput
11.  7 barry.txt
```

We can instead get the new data to be appended to the file by using the double greater than operator ( >> ).
```bash
12.  $ cat myoutput
13.  7 barry.txt
14.  $ ls >> myoutput
15.  $ cat myoutput
16.  7 barry.txt
17.  barry.txt
18.  bob
19.  example.png
20.  firstfile
21.  foo1
22.  myoutput
23.  video.mpeg
```
## Redirecting from a File

If we use the less than operator ( < ) then we can send data the other way. We will read data from the file and feed it into the program via it's STDIN stream.
```bash
$ wc -l myoutput
8 myoutput
$ wc -l < myoutput
8
```

A lot of programs (as we've seen in previous sections) allow us to supply a file as a command line argument and it will read and process the contents of that file. Given this, you may be asking why we would need to use this operator. The above example illustrates a subtle but useful difference. You'll notice that when we ran wc supplying the file to process as a command line argument, the output from the program included the name of the file that was processed. When we ran it redirecting the contents of the file into wc the file name was not printed. This is because whenever we use redirection or piping, the data is sent anonymously. So in the above example, wc recieved some content to process, but it has no knowledge of where it came from so it may not print this information. As a result, this mechanism is often used in order to get ancillary data (which may not be required) to not be printed.

We may easily combine the two forms of redirection we have seen so far into a single command as seen in the example below.
```bash
$ wc -l < barry.txt > myoutput
$ cat myoutput
7
```
## Redirecting STDERR

Now let's look at the third stream which is Standard Error or STDERR. The three streams actually have numbers associated with them (in brackets in the list at the top of the page). STDERR is stream number 2 and we may use these numbers to identify the streams. If we place a number before the > operator then it will redirect that stream (if we don't use a number, like we have been doing so far, then it defaults to stream 1).
```bash
$ ls -l video.mpg blah.foo
ls: cannot access blah.foo: No such file or directory
-rwxr--r-- 1 ryan users 6 May 16 09:14 video.mpg
$  ls -l video.mpg blah.foo 2> errors.txt
-rwxr--r-- 1 ryan users 6 May 16 09:14 video.mpg
$ cat errors.txt
7.  ls: cannot access blah.foo: No such file or directory
```

Maybe we wish to save both normal output and error messages into a single file. This can be done by redirecting the STDERR stream to the STDOUT stream and redirecting STDOUT to a file. We redirect to a file first then redirect the error stream. We identify the redirection to a stream by placing an & in front of the stream number (otherwise it would redirect to a file called 1).
```bash
$ ls -l video.mpg blah.foo > myoutput 2>&1
$ cat myoutput
ls: cannot access blah.foo: No such file or directory
-rwxr--r-- 1 ryan users 6 May 16 09:14 video.mpg
```
## Piping

So far we've dealt with sending data to and from files. Now we'll take a look at a mechanism for sending data from one program to another. It's called piping and the operator we use is ( | ) (found above the backslash ( \ ) key on most keyboards). What this operator does is feed the output from the program on the left as input to the program on the right. In the example below we will list only the first 3 files in the directory.
```bash
$  ls
barry.txt bob example.png firstfile foo1 myoutput video.mpeg
$ ls | head -3
barry.txt
bob
example.png
```
We may pipe as many programs together as we like. In the below example we have then piped the output to tail so as to get only the third file.
```bash
$ ls | head -3 | tail -1
example.png
```
I often find people try and write their pipes all out in one go and make a mistake somewhere along the line. They then think it is in one point but in fact it is another point. They waste a lot of time trying to fix a problem that is not there while not seeing the problem that is there. If you build your pipes up incrementally then you won't fall into this trap. Run the first program and make sure it provides the output you were expecting. Then add the second program and check again before adding the third and so on. This will save you a lot of frustration.

## Summary

`>` Save output to a file.

`>>` Append output to a file.

`<` Read input from a file.

`2>` Redirect error messages.

`|` Send the output from one program as input to another program.

Every program you may run on the command line has 3 streams, STDIN, STDOUT and STDERR.

## Sources
- https://ryanstutorials.net/linuxtutorial/piping.php

