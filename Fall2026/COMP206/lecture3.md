# COMP 206 — Lecture 3

**Course:** Introduction to Software Systems  
**Date:** September 8th 2026
**Topic:** Shell

---

## Shell
- The **shell** is a program that provides users access to the system on which it runs
  - It provides a way to get user input (i.e. the command-line), displays OS information, and stores session information (e.g. the previous command you ran)
- There are many shells:
  -sh, bash (most common Linux shell), zsh (default for macOS), PowerShell, cmd.exe
  - We will use Bash (which is the default on mimi)
- The **terminal** emulator lets you send keyboard input to the shell and displays text from the shell

## Command-line interface
i.e.: mberub20@teach-node-08:~/comp206_f2026$ __________

All of that is called the **prompt** and the remaining space is for the **user input**

- mberub20: username
- @: seperator between username and hostname
- teach-node-08: hostname
- **:**: seperator between user and current directory
- ~/comp206_f2026: current directory
- $: indicates the end of the prompt and the start of the user input
- empty space: the user input

**Input format:** Command flags arguments (order of flags and arguments is not always strict)

- Command: The program to run
- Flags (Also called switches or options): modifies behaviour of the command
- Arguments (also called parameters): input passed to the command

The root is the top folder of the OS, special symbol: **/**

The home directory is the top folder in the user's directory tree, special symbol is: **~**

The current directory (also called the **working directory**) has the following special symbol: **.**

The parent directory (the directory "above" the current directory) has the following special symbol: **..**

## The truth about Unix files and directories
- Philosophy: Everything is a file
- Directories are simply a special type of file that contains a list of index nodes (inodes):
  - Index nodes contain metadata about a file, including wheter it's a regular file or directory (or other special types), who owns it, the permissions, etc., and the location of the file on the disk
  - Will not discuss inodes much, but good to keep in mind
- Unix does not impose any file structure (file format) to regular files. Their structure and the way to interpret them is entirely dependent on the software using them.
  - File extensions mean nothing and are only useful for the user. Different from Windows!

## First UNIX file manipulation commands
### ls
- Description: List directory content
  - List information about the FILEs (current directory by default). Sort alphabetically by defaul
- Syntax: ls [OPTION]... [FILE]...
  - brackets means optional, and ... means there may be multiple
- Common flags (options):
  - **-l**: see contents in long format
  - **-a**: do not ignore hidden files (files that start with .)
Examples:
- List contents of current directory:
  - ls
- List contents of /etc/network
  - ls /etc/network
  - ls network (if currently in /etc)

### mkdir
- Description: Make directions
  - Create directories if they do not already exist
- Syntax: mkdir [OPTION]... Directory...

### touch
- Description: Makes an empty file
  - The original purpose of touch is to update a file timestamp, but a side-effect is that it creates the file if it does not exist, which became its most common uses
- Syntax: touch [OPTION] FILE

### rm
- Description: Remove files or directories
- Syntax: rm [OPTION]... [FILE]...
- Common flags:
  - **-r or -R**: recursively visits a directory, first visiting the files and subdirectories beneath it
    - necessary to delete directories!
- Important: No recycle bin!

### mv
- Description: Move files or directories
- Syntax:
  - mv [OPTION]... SOURCE DEST
  - mv [OPTION]... SOURCE... DIRECTORY
- Move source to destination, or source(s) to directory
  - If the last argument is a directory, will move files to that directory!
  - Otherwise, it moves and rename the file/directory
- Important: Does not ask before overwriting!

### cp
- Description: Copy files or directories
- Syntax:
  - cp [OPTION]... SOURCE DEST
  - cp [OPTION]... SOURCE... DIRECTORY
- Copy source to destination, or source(s) to directory
  - If the last argument is a directory, will copy files to that directory!
  - Otherwise, it copies and rename the file/directory
- Important: Does not ask before overwriting!
- Common flags:
  - **-r or -R**: recursively visits a directory, first visiting the files and subdirectories beneath it
    - necessary to copy directories

### cat and more
- cat [OPTIONS]... FILE...
  - file concatenate and display the concatenated result
- more [OPTIONS]... FILE...
  - page through a text file

### man
- allows you to access the on-line manual pages of the various commands available on the shell
  - These pages are often referred to as "man pages"
- The man pages are your first source of information when working in the shell
- To acces a man page, simply type man and the name of the command at the prompt
- i.e. man ls