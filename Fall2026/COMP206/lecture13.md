# COMP 206 — Lecture 13

**Course:** Introduction to Software Systems  
**Date:** October 20th 2026
**Topic:** Libraries, Arrays, Pointers

---
# Libraries
- They are a collection of functions
- C standard lib provides basic I/O (stdio.h), string manipulation (string.h), memory allocation (stdlib.h) and otehr basic functionallity to C programs.

In C, functions must be declared before being used.
- Compiler needs to know the return type and the argument types

We will mostly use these standard header files:
- <ctype.h>: Function to manipulate characters (e.g convert between upper and lower case)
- <math.h>: Common mathematical functions
- <stdio.h>: I/O functions
- <stdlib.h>: Functions to handle memory allocation, and also number conversions and random number generation
- <string.h>: Stirng-handling functions

## stdio.h
Some functions:
- getc, putc, and puts
- getchar, putchar
- fgets
- printf
- scanf
- sprintf
- sscanf
- Functions for file manipulation (fopen, fprintf, fputs, fputc)

## Format specifiers
The percentage character is used for formats specifiers
- Format: %[flags][width][.precision][length]specifier
    - Specifiers (some examples):
        - c: character
        - d or i: signed decimal integer
        - f: float
        - s: string
    - Flags (some examples):
        - -: Left-justify the width (default is right)
        - +: precede positive numbers with a plus
    - The width is the min number of characters to be printed, pads with blank space
    - The precision is a number to specify the min number of digits
    The length is for type swith length modifiers like short ('h') or long ('l')

Examples:
``` C
int age = 12;
printf("I am %d years old.\n", age);
printf("I am %10d years old.\n", age);
printf("I am %-10d years old.\n", age);
```

## Arrays
### One-Dimensional Arrays
TYPE NAME[SIZE];
``` C
int a[10];
char name[30];
```

When array initializer is used, size can be omitted.

int a[] = {4, 3, 5, 1, 2}

### Multi-Dimensional Arrays
TYPE NAME[ROWS][COLS];

Intializer:
``` C
int a[3][5] = {{5, 4, 3, 1, 3},
               {5, 2, 5, 6 ,4},
               {7, 4, 6, 4, 2}};
```

## Pointers
Memory is divided into bytes (8 bits)

Each byte has an address

Each variable in a program occupies one or more bytes in memory. (i.e. 4-bytes int i located at address 200)

The first byte is the address of the variable

A pointer variable stores the address of a variable

If we have a variable i, and we store its address in pointer variable p, we say that p points to i

Example:
Let's say that we have an int variable that contains 5 and its addrtess is 1096. Then pointer p contains the location of x. Note how the pointer itself has its own address.

### Declaring a pointer variable
To declare a pointer variable, the identifier is preceded by an asterisk in the decleration.

Syntax: TYPE *VARIABLE;

### Address-of operator (&)
The address-of operator (&) returns the address of a variable.

As such, to make a pointer point to a variable, we do the following:
``` C
int i;
int *p;
p = &i;
// We could also do it right away:
int i;
int *p = &i;
```

### Deference operator (*)
Also called indirection operator. When a pointer vaeriable points to an object, we can use * to access what is stored in the object. For example:
``` C
int i;
int *p;
p = &i;
i = 5;
printf("%d", i); // prints 5 to the screen
printf("%d", *p); // prints 5 to the screen
*p = 2;
printf("%d", i); // prints 2 to the screen
printf("%d", *p); // prints 2 to the screen

