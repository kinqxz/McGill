# COMP 206 — Lecture 7

**Course:** Introduction to Software Systems  
**Date:** September 22nd 2026
**Topic:** Bash Control Structures

---

## Not mentioned last time

As we saw, we can access the value of varialbe name with $name
An alternate way is ${name}


## Other positional variables

- System parameters:
  - $#: number of arguments on the command line
  - $-: options supplied to the shell
  - $?: exit value of the last command executed
  - $$: process number of the current process
  - $!: process number of the last command done in background
- Command-line parameters:
  - $n: where n is from 1 through 9, reading left to right
    - ${10}, ${11} ...
  - $0: the name of the current shell or program
  - $*: all arguments on the command line "$1 $2 ... $9" as a string
  - $@: all arguments on the command line ("$1", "$2", ..., "$9") as an array

## Quoting

- Single quotes (') are used to preserve the literal value of characters within the quotes
- Double quotes (") are used to preserve the literal values of characters within the  quotes, except $, ` and \
- In both cases, the space character is preserved.

## Quotes and variables
- The same applies to variables

## Escape characters
- The blackslash (\) is Bash's escape character
- It preserves the literal value of the next character that follows
- With some commands and some characters, it can instead toggle on a special meaning for the character:
- For example, when using echo -e
  - \n means newline
  - \r means return
  - \t means tab

## Control flow
### Exit status
- Any program, when it exists, gives a status code back to the OS to signal whether the command succeeded or failed.
- Code 0 means success, and any other code means failure
- You an end a script by using the exit command, optionally specifying a status code, e.g. exit 1

## Running commands one after anohter
- There are miultiple ways to chain commands together
  - One way that we saw is redirection/piping
  - Another way that we saw is to write a script, where each line is executed one after the other
- Another way is the semicolon (;), with the same meaning as an ew line in a script:
  - mkdir my_dir ; cd my_dir # runs mkdir my_dir, then cd my_dir

## If statement
if COMMAND
then
    ...
elif COMMAND
then
    ...
else
    ...
fi

## While loop
while COMMAND
do  
    ...
done

## Comparison (test)
- Often, we want a condition in an if-statemtn or while loop to check if two variables are equal, or if a variable is equal to a particular string, etc.
- The command for this is called test