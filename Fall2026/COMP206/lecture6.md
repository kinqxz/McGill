# COMP 206 — Lecture 6

**Course:** Introduction to Software Systems  
**Date:** September 17th 2026
**Topic:** Bash scripting

---

## Bash Scripting
- So far, we have used Bash in interactive mode
  - Commands are read from command-line
- The Bash shell supports the execution of commands from files (non-interactive mode)
  - Lets user or system automate common sequences of commands
- These files are called scripts
- Scripts are run in a similar way to any programming language
  - Scripting languages are interpreted (as opposed to compiled): code is executed directly without being compiled to machine code

Example:

#!/bin/bash
mdkir my_dir
cd my_dir
touch my_file.txt
ls

## Shebang
- File type is not determined by file extension in Unix
  - Convention is that Bash scripts use file extension .sh, but this is only a visual indicator for humans!
- To run a Bash script (for example, comp206/my_script), one way would be to give the script as input to the Bash interpreter:
  - bash comp206/my_script
  - Compare: If comp206/my_script was a python3 program instead, we would use
    - python3 comp206/my_script
- This is not how we usually run Bash scripts!
- We can also tell the OS which interpreter the file should be run with by using a shebang
- The shebang is the very first line of the file: It consists of a hash symbol, followed by an exclamation mark, followed by the path to the interpreter
- For Bash, this is: #!/bin/nash
  - Compare: for python3, this would be #!/bin/python3
- Can now directly execute the file, and the OS will select the correct interpreter
  - i.e. can now simply type comp206/my_script instead of bash comp206/my_script
- All of your scripts should be run this way!

## Running a script
1. Give yourself execute permissions on the script
2. Type the path of the script to execute it, followed by the flags and arguments
- e.g. comp206/myprogram.sh arg1 arg2
- If the script is in the current directory, you must explicitely specify that it is in the current directory by using ./ at the front
  - e.g. ./myprogram.sh arg1 arg2

Why ./ in front?
- When typing the name of a program, the shell finds the program as follows:
  - if the name contains /, the shell assumes that this is a path (could be relative or absolute) and looks for the program at that location
  - If the name doesn't contain /, the shell looks in all the folders listed in a shell variable called PATH (more on that in later class)
    - try echo $PATH
    - For example, when running ls, the shell finds that command in /usr/bin/ls
- Looking at the rules aboves, this implies that we are unable to refer to a program in the current directory (and not in PATH) by using a relative path without /
  - This is by design: What if someone maliciously named a virus "ls"

## When are scripts used? (Examples)
- Login scripts (Run automatically at login)
  - Write scripts to help you get to where you want to go
  - Write scripts to customize the environment
- During development and testing (Run manually during session)
  - Write scripts that help you to
    - Compile quickly and manage errors and executing the program
    - Copying to and from repository
    - Making your own local backups
    - Help run testing (repeated tasks, good candidate for automation)
- Logout scripts (Run automatically at logout)
  - Write scripts to do housekeeping
    - Automating backup procedures
    - Automating the logging of events
    - Automating the deletion of files (empty trash)

## Example: Writing a script
- Want to make a script that will move all my txt files to a directory called textfiles and all my doc files to a directory called docfiles

$ vim move.sh
$!/bin/bash (shebang)
.# Move txt and doc files from curr dir (comment without the .)
.# to new dirs txtfiles and docfiles (comment without the .)
mkdir txtfiles
mkdir docfiles
mv *.txt txtfiles
mv *.doc docfiles
$ chmod +x move.sh
$ ./move.sh

## Variables
- Variables are assigned using the syntax name=value
  - Important: no space before and after equal sign!
- To user a variable, $name is used
- Examples:
  - str="hello world"
  - num=5
  - date=$(date) # what does this do?
  - echo $str
  - echo $num
  - echo $date

## Positional variables
- Parameters passed to a bash script (e.g. on the command line) are numbered from $1
- For examples, if we run ./script 5 2 Bob
- From the script we can access 5, 2, Bob using $1, $2, $3