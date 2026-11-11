# COMP 206 — Lecture 16

**Course:** Introduction to Software Systems  
**Date:** October 29th 2026
**Topic:** Functions (cont.), More Standard Utilities, Structs and Unions

---
## scanf
int scanf(char *format_str, pointer_aguments...);

## sscanf
Identical to scanf, except that it reads from a string instead of reading from stdin

int sscanf(char *source_str, char *format_str, pointer_arguments);

## sprintf
See slides

# Structs and unions
Structures (struct) are a collection of items that may have different types. Its elements are called members, and unlike arrays, they are accessed by name.

Ex:
``` C
#include <stdio.h>
#include <string.h>
struct {
    char name[30];
    int age;
    float salary;
} a; // notice the semi-colon

int main(void) {
    a.age = 25;
    strcpy(a.name, "John");
    printf("%s is %d years old\n", a.name, a.age);
}
```

Tags solve the problems from the previous example. The tag (`PERSON`) names the struct type, so the member list is written once and later declarations just use the tag.

``` C
#include <stdio.h>
#include <string.h>
struct PERSON { // PERSON is the tag
    char name[30];
    int age;
    float salary;
}; // semi-colon even though no variable is declared here

int main(void) {
    struct PERSON a; // tag replaces the member definitions
    // ...
    struct PERSON b;
}
```

## Union
Syntax:

union OPTIONAL_TAG {
    FIELDS;
};

It is similar to struct in syntax, but only one object is storead at the same time.

