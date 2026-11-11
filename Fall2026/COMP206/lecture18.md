# COMP 206 — Lecture 18

**Course:** Introduction to Software Systems  
**Date:** November 3rd 2026
**Topic:** Dynamic Memory

---
# Some stdlib.h functions
long strtol(char *str, char **endptr, int base);
- converts str to a long integer
- endptr is apointer to the char after it stopped reading the string: this can be NULL if you do not need this
- base: the base of the integer: if this is 0, it interprets the string the same way as integer constants (e.g. "50" would be interpreted as base 10 and "0x50" would be interpreted as hexadecimal)
- There are similar functions for doulbe (strtod), float (strof), long long (strtoll). For int, you should simply use strtol

int system(char *str);
- Executes a shell command
- Example: system("ls");

int x = rand(void);
- Returns a random number between 0 to RAND_MAX, a macro defined in stdlib.h (at least 32767)
- To get a value between 0 and N, you can do
- int value = rand() % (N + 1);

int abs(int x);
- Get the absolute value

void exit(int status);
- Stop the program and send status code to OS

# C's dynamic memory functions
void *malloc(size_t size);
- Allocates a block of size size in memory and returns a pointer to it
- Does not initialie it
- This is the most used allocation function

void *calloc(size_t num, size_t size);
- Allocates a block of size size * num in memory and return a pointer to it
- Initializes it by setting all bits to 0
- Like malloc, calloc returns a void pointer

void free(void *ptr);
- Releases the block of memory pointed by the pointer (needs to ahve been previously assigned by a memory allocation function, not just any pointer)
- As long as you dont do this, the memory is not release. Anytime you malloc, you will need to release it later. C doesn't have automatic garbage collection.

## Example: allocating storage for an uninitialized array
``` C
#include <stdio.h>
#include <stdlib.h>

int main(void) {
    int *array;
    int n;

    scanf("%d", &n); // asking user for size of "array" at run-time
    array = malloc(n * sizeof(int)); // even if you know that sizeof(int) is 4 on
                                     // your machine, still good programming
                                     // habit to stick with sizeof

    if (array == NULL) exit(1);

    array[0] = 5;
    printf("%d", array[0]);

    free(array);
    return 0;
}
```

### Right allow selection
x->age = 5;

Is the same as: (*x).age =5; when accessing a field from a struct that has allocated space

## Linked Lists

### Node
A simple linked list node:

``` C
struct NODE {
    int data; // the data we want to store in the node
    struct NODE *next; // the pointer to the following node in the list
};
```

To keep track of where the list begins, we need a variable that always points to the first node (the head). With no node yet, set it to NULL to indicate the list is empty:

``` C
struct NODE *head = NULL;
```

### Creating a node
1. Allocate memory for the node
2. Store data in the node
3. Insert the node in the list

``` C
struct NODE *aNode; // variable that will temporarily point to the node until we insert it

// 1. Allocate memory for the node
aNode = malloc(sizeof(struct NODE));
if (aNode == NULL) exit(1);

// 2. Store data in the node
aNode->data = 5; // equivalent to (*aNode).data = 5;

// 3. Inserting the node is on the next slide
```

## Pointers to functions
Functions also have addresses, and you can point to them.

``` C
int sum(int a, int b) {
    return a + b;
}

void hello_world() {
    puts("Hello World");
}

int main(void) {
    int (*sumptr)(int, int); // pointer to a function that takes two ints and returns an int
    void (*helloptr)(); // pointer to a function that takes no argument and returns nothing

    sumptr = &sum;
    helloptr = &hello_world;

    int x = (*sumptr)(10, 5);
    (*helloptr)();
}
```