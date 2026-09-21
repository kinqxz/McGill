# COMP 206 — Lecture 4

**Course:** Introduction to Software Systems  
**Date:** September 10th 2026
**Topic:**  Wildcards & Redirection

---

**pwd**: print working directory
Flags can be combined: ls -la == ls -l -a
less: updated version of more
cp usage: cp ex.txt Docs/ex.txt or cp ex.txt Docs

Options for cp, mv, and rm:
- i: interactive: prompt and wiat for confirmation before proceeding
- -r or -R: recursive(cp, rm): recusrsively visits a directory, first visiting the files and subdirectories beneath it - This is how you copy or remove directories
- -f : force (mv, rm): don't prompt for confirmation (overrides -i if placed after)

typing **history** will show you list of commands you used

You can exit a shell by using **exit** or sign-out from mimi with **logout** 

Terminate programs by force with Ctrl+C
Ctrl+D stop waiting for an input

## Wildcards
- A wildcard is a symbol used to replace one or more characters in a filename. In Bash, these are:
- The "asterisk": Any pattern
  - *.doc
- The "question mark": Any single character
  - ?at.doc
- The "square brackets": Any character within the brackets
  - cat.d[aoz]c
  - [a-d] == [abcd], [!a] any single character except letter a

## Filename expansion (globbing)
- The shell recognizes and expands wildcards patterns into the list of pathnames matching the pattern. This is called **globbing**
- As the shell always does this when interpreting your input, this works for all the commands you've seen
- For example, if you type ls *.doc in a directory with the files on the right, you will see all the files that end with .doc files in your directory. If you tpye rm ?at.doc you will remove cat.doc and bat.doc

Who globs?
- The shell expands the wildcard patterns before giving them as arguments. For example, if you type ls *.doc the shell expands it into ls john.doc cat.doc bat.doc (The command has no idea that you used wildcards, the shell is the one doing the work)
- You can see this by yourself with the echo command: try echo ls *.doc in a directory with doc files.

## Precisions on globbing
- Note that if a filename starts with a dot (i.e. is hidden), it must be matched explicitly
- For example, *.txt does not match .hidden.txt
  - but .*.txt does
- Globbing is applied on each segments of a pathname seperately (i.e. each parts seperated by /). For example, if you are in comp206 directory below and want to match Docs/myfile.txt, typing *.txt would not match it. However, Docs/*.txt or */*.txt would match it.

## If wildcards can't be matched
- If the wildcards can't be matched, the shell itself won't do anything with them or send an error message, and the wildcards will simply be sent to the command literally
- For example, in a directory with no .dic files, echo ls *.doc will echo back ls *.doc and ls will think you're trying to open a file literally called *.doc
- This can cause unexpected results

## Command substitution
- The shell can also subtitue the outputs of commands
- Syntax: $(command)
- Exmaple: touch $(date +%Y-%m-%d).txt
  - the shell first runs date +&Y-%m-%d
    - date is a command that outputs today's date. +%Y-%m-%d specifies the format should be YYYY-MM-DD
  - The output of this command today is 2026-09-10
  - The shell replaces $(date +%Y-%m-%d) by 2026-09-10
    - i.e. the command becomes touch 2026-09-10.txt
  - touch creates file 2026-09-10.txt

## Redirection
Standard streams
- Communication channels between a computer program and its environment when it begins execution
- The three standard streams are:
  - STDIN (Standard In): this is the channel were keys typed by the user are gathered
  - STDOUT (Standard Out): this is the channel where normal application output is sent
  - STDERR (Standard Error): this is the channel where error output is sent
- Normal outpout and error output is seperated on two diferent channels since they are often monitored in different ways.

## File descriptors
- When a file is opened, Unix creates a unique identifier called a file descriptor to refer to that file.
  - File descriptior table keeps tracks of all files currently open
- Unix has three special file descriptors which are always opened, and always have the same index in the file descriptor table, representing the three standard streams:
  - File descriptor 0: STDIN (Standard In)
  - File descriptor 1: STDOUT (Standard Out)
  - File descriptor 2: STDERR (Standard Error)

## Redirection Part 2
- By default:
  - stdin goes from keyboard to program
  - stdout and stderr goes from program to display
- But can redirect these streams!

Redirect stdout to a file instead of display:
- Symbol: **>**
- Ex: ls -la > list.txt

Variant: append to existing file instead of overwriting
- Symbol: **>>**
- Ex: ls -la >> list.txt

Redirect stdin from a file instead of keyboard:
- Symbol: **<**
- Ex: my_program < input.txt

Redirecting stdout from a program to stdin of a program has a special name: **Piping**
- Symbol: | (called pipe)
- Ex: ls -l | more

Chaining!
Redirection and piping can be chained together to make complex commands
- Ex: Get input from file, and output to another file
  - my_program < input.txt > output.txt
- Ex: Pipe and redirect output to file
  - ls -l | head > output.txt (head shows the first 10 lines)

Another example
- cat $(ls *.log | tail -n5) >> text.out
  - Assume we have files f1.log f2.log ... f20.log
