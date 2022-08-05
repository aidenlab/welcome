# Beginner Terminal tips

Notes taken by: Michael Ngo

## Basic Commands:

- pwd
    - **print working directory** (full path)
- open [directory/file name]
    - opens directory in finder (or opens up file)
- ls
    - **list**s all directories and files in the directory you’re in now
- cd [directory name/folder]
    - **change directory**
    - cd .. / . / ~ / - / “/”
        - .. : parent directory
        - .  : means current directory
        - **~** : **home directory** (directory of whatever user is logged in)
        - - : previous directory
        - /   : root (of drive) directory (contains all other directories/files. At the highest level)
- clear
    - clears terminal screen. “cmd + k” does the same
- touch [filename]
    - creates a new file (in the working directory) of the file extension you wrote
- history
    - displays history of commands
- rm [filename]
    - **remove** file
    - note: rm, when deleting a directory, expects an option
        - **rm -r** (which stands for recursive) is used to delete directories. Removes directory and contents
    - note: rm does not send things to trash. They are deleted directly
- mkdir [directoryname]
    - **make directory**
- cp [sourcefile] [targetfile or dir]
    - **copy** file to file/directory
    - cp -r
        - recursive for copying directories and content within that directory
- mv [path to originalfilename] [path to newfilename]
    - **move** file to another directory
    - this can also be used to **rename** files if you move an existing file to a non-existing filename
- man [command]
    - **manual**: it lists all options available for that program. (e.g., “man rm” will display a list of all the rm options, one of which is rm -r for removing directories)
    - TIP: simply press “**q**” to exit a out of an open man page properly
    

- cat [file]
    - displays content of file directly in terminal
- head [file]
    - displays first 10 lines of file (can be run on multiple files at once)
    - with -n [num lines] flag and flag argument you can specify how many lines to display
- tail [file]
    - complement of head. Displays LAST N lines of file(s)

More niche Commands:

- top
    - displays active processes (press q to quit)
- pip list
    - to see what pip has installed (check for packages)

## **when editing in Vim**

(Unix text editor), which will happen when you do something like git commit without -m “[message]” or when trying to submit commands for a supercomputing cluster…

- vim [filename.filetype]
    - opens the file in Vim
- pressing **Esc** switches Vim to Normal mode, pressing **colon** in Normal mode switches Vim to Command Line mode, and pressing **i** takes you into Insert mode
- :q!
    - quits the Vim editor without saving
- :wq
    - saves the file
    - NOTE: must first be in Normal mode (Esc) to then enter Command Line mode (colon)
    
- :set number
    - displays line numbers
- :[number]
    - takes you to that line (if you don’t want to use arrow keys)
- :$
    - takes you to bottom line
    
- editing in Normal mode: **dd** deletes a line, holding **v** and then using arrow keys highlights text, **y** while the text is highlighted is “yank mode” and it copies the text to the clip board. **o** creates a new line, and to paste go to Normal mode (Esc) and hit **p** for paste
- :/SEARCH_KEYWORD searches for a word. **n** goes to next instance of that word

Notes:

- the command line is what you write in (the actual line itself), the Terminal is the overall command line interface (text input environment). Sometimes Terminal is called the command line though
- the prompt (is what’s usually on the very left. Has computer name and personal name and often ends with “$”. When you look at online tutorials, they’ll abbreviate the prompt with just “$”. You don’t ever write that $ in yourself when trying to follow those tutorials
- **commands** consist of **program, option (aka flag), argument** (but doesn’t always need option and argument)
    - NOTE ABOUT OPTIONS/FLAGS: options are prefixed by hyphens (”-”). Use double hyphen -- to specify a single multi-character option since after a single hyphen -, each subsequent letter is read as its own single character option.
        - -czf specifies three single-character flags: c, z, and f
        - --help specifies one multi-character flag: help
- typing “/” at end of a filename or directoryname is often a choice and negligible, but I believe it indicates that this file should already exist. In some cases (like copying a file) if you don’t have “/” at the end and you have a typo somewhere in the filename, you may mistakenly create a new file  (I think)
- CLI (command line interface) as opposed to GUI (graphical user interface)
    - Shell is what we use to interact with a computer. Also known as UI, the shell exposes the tools of the operating system to the human user. CLI and GUI are two types of shells (I think)
- Ctrl + c: kills whatever you are running (and clears current line)
- Ctrl + z: suspends process
- Ctrl ****+ w: cut one word backwards
- to change directory to something like Users, must include a “/” at the start to indicate root directory first, then Users
- Absolute vs Relative paths:
    - Absolute path: you can navigate to any directory/file from any working directory using an absolute path (address goes from root directory, Users, etc.)
    - Relative path: starts from current directory/folder
        - tip: can use relative path with “../” to first go to parent directory of current directory then can access directories on the same level as current directory
            - ../ can also be nested as ../../ to get parent of parent
- nano [filename]
    - opens file in nano editor so you can make quick changes to text directly through command line (note: in this interface, things like “cmd + s” don’t work to save. Use commands at bottom. ^ key indicates control key, NOT command)
    - note: I prefer using Vim
    
- pip stands for “Package Installer for Python”
- Homebrew is a free package management system that simplifies the installation of software on Apple’s operating system

Tips:

- “tab completion”: if you start typing a directory or file name, hitting tab will complete the name.
    - If two files have in common what you had started to type, nothing will happen. If you hit tab twice, it will list all files which start with that
- to move through history of terminal, use up and down arrow
- if you want to access/modify a child directory without actually changing into it, type [childDirectoryName] SLASH [filename] (i.e., type out it’s path, whether that be relative or absolute)
    - touch [directoryname/filename]
    - ls [childDirectoryName]
- **screen** command to open up what’s essentially another tab of terminal. In this separate tab, you can run commands that will run in the background when you do:
CMD + A then CMD +D
 to get back to the main terminal.
    - To view the other screen, type: 
    “screen -r” 
    for screen redirect to other screen. If you have multiple screens open at once, you can tab complete to find the IDs for the different screens