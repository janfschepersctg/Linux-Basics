# File Manipulation
### mkdir

`mkdir` (make directory) is used to create a directory.
```
$ ls
apple.txt foo/ somefiles.txt

$ mkdir bar
$ ls
apple.txt bar/ foo/ somefiles.txt
```
### mv

To move files, the command `mv` (move) is used.
```
$ ls
apple.txt bar/ foo/ somefiles.txt

$ mv apple.txt foo

$ ls
bar/ foo/ somefiles.txt

$ ls foo
apple.txt
```
Interestingly, it can also be used to rename things as well!

```
$ cd foo
$ ls
apple.txt

$ mv apple.txt hello.txt
$ ls
hello.txt
```
And if you’re tired of typing `ls` everytime after the command, a semicolon can condense your code into one line. This produces the same effect:

```
$ mv apple.txt hello.txt; ls
hello.txt
```
### rm

`rm` (remove) removes files. Take note that this action cannot be undone.

```
$ cd ..
$ ls
bar/ foo/ somefiles.txt

$ rm somefiles.txt
rm: remove regular file ‘somefiles.txt’? (y/n) y

$ ls
bar/ foo/
```
`rm` cannot be used with directories, unless accompanied by `-r` flag (short for _recursive_). What this means is that `rm` will go into every directory in the specified path and delete files one by one, recursively up each directory inside. If you don’t understand this, it’s fine, unless you do programming. Just remember that it deletes all the files and directories in the specified path.
```
$ ls
bar/ foo/

$ rm -r foo
rm: remove regular file ‘apple.txt’? (y/n) y
rm: remove ‘foo’? (y/n) y

$ ls
bar/
```
If you’re tired of typing `y`s for all the files, `rm -rf` can help you. Be extremely careful, however, as this command-flag combination is incredibly dangerous. If you accidentally type the wrong path — boy, there’s no going back!

### touch

When you wish to create new (empty) files, use `touch`.

```
$ ls
$
$ touch file1 file2.txt file3
$ ls
file1 file2.txt file3
```
### cp

Copying is undeniably one of the greatest inventions of all time. To do that, use `cp` (copy).
```
$ ls
file1 file2.txt file3

$ cp file2.txt file2copy.txt

$ ls
file1 file2.txt file2copy.txt file3
```

To copy a directory recursively, use `cp -r`.

## Sources
https://www.pluralsight.com/guides/beginner-linux-navigation-manual
