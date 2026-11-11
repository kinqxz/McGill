# COMP 206 — Lecture 11

**Course:** Introduction to Software Systems  
**Date:** October 8th 2026
**Topic:** Introduction to C

---

# Basic Structure of a C Program

``` C
/* Hello world program */
#include <stdio.h>
int main(void)
{
    puts("Hello World");
    return 0; // error code
}
```

Another example:
``` C
#include <stdio.h>
int main(void)
{
    char c; // declaring a variable

    puts ("Freshman: ");
    c = getc(stdin); // initializing the variable

    if (c == 'Y' || c == 'y') // using the variable
        puts ("Welcome\n");
    else
        puts("Sorry, try again.\n");
    
    return  0;
}
```

STDIO.H is the standard in/out lib. The previous code uses two functions from it:

puts(): writes strings

getc(): reads a character

The main function has a return type int, and it is the error code that is being returned.

## gcc

GNU Compiler Collection
usage: gcc FLAGS FILES

### Flags
Without a flag the default outcome is to compile all the files into a single executable file named a.out

-o Replace the default a.out file name with your own (i.e. gcc helloworld.c -o hello)

## How to compile and run a C program

- vim helloworld.c
- gcc helloworld.c
- ./a.out

## Escape characters
- \n (New line)
- \r (Carriage return)
- \t (Tab)
- \\ (Backslash)
- \b (Backspace (non-destructive))


## GCC and errors
You will have some long error messages that you might want to keep, so the solution is: gcc helloworld.c 2> textfilename

All error messages from gcc will be stored in the textfilename file. You can then use vim, more, less, or cat to view the contents.

Trust only the first couple of errors since they are made by assumption and the remaining ones could be false.

## Command Line Processing
``` C
int main(int argc, char *argv[]) {
    // argc     is like $#
    // argv[1]  is like $1
    // argv[2]  is like $2, etc.

    int n;

    for (n=0; n < argc; n++)
        printf("%s\n", argv[n]);

    return 0;
}
```

