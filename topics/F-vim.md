# VIM Basics
## Introduction
Before we start writing a basic bash script, we will learn one of the most proficient tools for editing files: vim.

## Features of Vim

This section discusses some of the important features of Vim −

-   Its memory footprint is very low
    
-   It is command centric. You can perform complex text related task with few commands
    
-   It is highly configurable and uses simple text file to store its configuration
    
-   There are many plug-in available for Vim. Its functionality can be extended in great manner using these plug-in
    
-   It supports multiple windows. Using this feature screen can be split into multiple windows
    
-   Same as multiple windows, it also supports multiple buffers
    
-   It supports multiple tabs which allows to work on multiple files
    
-   It supports recording features which allows to record and play Vim commands in repeated manner

## Using vim
### Starting vim
just type `vim` in the console.
You can open a file (or multiple) with the command: `vim $file1 $file2 $file`

### Understanding vim modes
vim supports multiple modes. This section discusses some of the important modes which will be used on day-to-day basis.

#### Command mode

This is the default mode in which Vim starts. We can enter editor commands in this mode. We can use variety of commands in this mode like copy, paste, delete, replace and many more. We’ll discuss these commands in later sections.

**NOTE − Here onwards, any Vim command without colon indicates that we are executing that command in command mode.**

#### Insert mode

You can use this mode to enter/edit text. To switch from default command to insert mode press i key. It will show current mode in bottom left corner of editor.

Use Escape key to switch back to command mode from this mode.

### Command line mode

This mode is also used to enter commands. Commands in this mode starts with colon(:). For instance, in previous section quit command was entered in this mode. We can go to this mode either from command or insert mode.

-   To switch from command mode to this mode just type colon
    
-   To switch from insert mode to this mode press Escape and type colon

### Visual mode

In this mode we can visually select text and run commands on selected sections.

-   To switch from command mode to visual mode type v
    
-   To switch from any other mode to visual mode first switch back to command mode by pressing Escape, then type v to switch to visual mode

## Cheat sheet
Link to a very extensive cheat sheet: https://devhints.io/vim

Commands work in normal mode, unless specified explicitly.

## Movement

| Key          | Action                                             |
| :---         | :---                                               |
| `0` / `$`    | Begin/end of line                                  |
| `w`,  `W`    | start of next word (`W` ignores punctuation)       |
| `e`,  `E`    | end of next word (`E` ignores punctuation)         |
| `b`,  `B`    | backwards by word (`B` ignores punctuation)        |
| `f + $char`,  `F + $char`    | forwards/backwards to the first encountered character        |
| `h`,  `j`, `k`, `l`   | left, down, up, right (use this instead of the arrows)      |
| `gg`,  `G`  | beginning of file / end of file      |


## Cut/Copy/Paste

| Key                         | Action                                         |
| :-----------                | :-----------------------                       |
| `x`                         | Cut letter                                     |
| `y` **movement**            | Copy                                           |
| `"ad` `"ay`                 | Cut/Copy to/from register 'a' (works  for a-z) |
| `p` `P`                     | Paste after/before cursor                      |
| `yy`                        | yank line                                      |


## Editing tricks

| Key               | Action                                      |
| :-----------      | :-----------------------                    |
| `%s/OLD/NEW/gc`   | Interactive search/replace                  |
| `%g/PATTERN/d`    | Delete lines matching PATTERN               |
| `gU` **movement** | Change to uppercase                         |
| `gu` **movement** | Change to lowercase                         |
| `g~` **movement** | Toggle case                                 |

## Exiting / saving
| Key                         | Action                                         |
| :-----------                | :-----------------------                       |
| `x`                         | save and exit                                   |
| `w`                         | save                                           |
| `q`                         | save exit |
| `q!`                         | save exit and disregard changes |

## Using Visual mode
| Key                         | Action                                         |
| :-----------                | :-----------------------                       |
| `v`                         | character mode                                |
| `V`                         | line mode                                           |
| `ctrl+v`                         | block mode |

# Sources
- https://devhints.io/vim
- https://github.com/bertvv/cheat-sheets
- https://www.tutorialspoint.com/vim/index.htm



