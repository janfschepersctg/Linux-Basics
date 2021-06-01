# Text processing

## Text Processing in Unix

Unix provides a number of powerful commands to process texts in different ways. These text processing commands are often implemented as filters.

Filters are commands that always read their input from ‘stdin’ and write their output to ‘stdout’. Users can use file redirection and ‘pipes’ to setup ‘stdin’ and ‘stdout’ as per their need. Pipes are used to direct the ‘stdout’ stream of one command to the ‘stdin’ stream of the next command.

Some standard filter commands are described below. These commands may also take an input file as a parameter, but by default when the file is not specified, they operate as filter commands.

The rich set of text processing commands is comprehensive and time saving. Knowing even their existence is enough to avoid the need of writing yet another script (which takes time and effort plus debugging) – a trap which many beginners fall into. An extensive list of text processing commands and examples can be found [here](http://tldp.org/LDP/abs/html/textproc.html)

## Most commong Filter Commands

-   **grep:** Find lines in stdin that match a pattern and print them to stdout.
-   **sort:** Sort the lines in stdin, and print the result to stdout.
-   **uniq:** Read from stdin and print unique (that are different from the adjacent line) to stdout.
-   **cat:** Read lines from stdin (and more files), and concatenate them to stdout.
-   **cut:** Cut specified byte, character or field from each line of stdin and print to stdout.
-   **head:** Read the first few lines from stdin (and more files) and print them to stdout.
-   **tail:** Read the last few lines from stdin (and more files) and print them to stdout.
-   **wc:** Read from stdin, and print the number of newlines, words, and bytes to stdout.

## Other resources worth reading
- https://learnbyexample.gitbooks.io/linux-command-line/content/Text_Processing.html
- https://tldp.org/LDP/abs/html/textproc.html

## Sources
https://learnbyexample.gitbooks.io/linux-command-line/content/Text_Processing.html



