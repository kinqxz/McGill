# COMP 206 — Lecture 14

**Course:** Introduction to Software Systems  
**Date:** October 22nd 2026
**Topic:** Pointers, Strings

---

## Type conversion
### Implicit type conversions
### Usual arithmetic conversions
- If one of the operands is a long double, the other is converted to long double
- If one of the operands is a double, the other is converted to double
- If one of the operands is a float, ...
- If both operands are not floating types, then they are promoted to be at least the size of int. If the operands still have different types, the samllest operand is converted to the bigger one according to this rank: (int<unsigned int<long<unsigned long<long long< unsigned long long).

(type) expression
Where expression is converted to type type

Ex:
float f = 2.5;
int i = (int) f

Type conversion has higher precedence than binary operators (i.e. division)

## Pointers
### Printing a pointer address
To print the address the pointer points to, you can use the %p specifier.

%p expects a variable of type void*

This is how the address itself (or offset) can be printed:
``` C
int i;
int *q = &i;
print("%p", (void*) q);
```

### Arrays + Pointers
The compiler reserves sizeof(type)*length bytes in memory starting from the base address.

You can point to an array by pointing to the address of its first element.

### Point arithmetic
- You can add an integer to a pointer
- subtract an integer from a pointer
- subtract a pointer from a pointer (if both point to the same array)

## String literals
- Sequence of chars between double quotes
- When a string literal of size n is written, the compiler stores it in some place in memory (might be read-only) as a character array of size n+1 (the n+1 char is the null character, which is '\0')

Ex: char c = "abcd"[1] // c ='b'

``` C
int main(int argc, char *argv[]) {
    // argc     the number of arguments,
    //          including the name of the executable
    //          i.e. in Bash this would be ($#+1)
    // Recall that char * is a string,
    // so char *argv[] is an array of strings
    // argv[0] is like $0 in Bash,
    //      i.e. the name of the executable
    // argv[1] is like $1, i.e. the first arg
    // argv[2] is like $2, i.e. the second arg, etc.
    int n;
    for(n=0; n<argc; n++)
        printf("%s\n", argv[n]);
    return 0;
}
```

## string.h
Important functions:
- int strcmp(char *s1, char *s2): compare two strings
- int strncmp(char *s1, char *s2, size_t num): Compare the first num characters of two strings
- size_t strlen(char *string): Returns the length of the string (does not include null terminator)
- char *strcpy(char *dest, char *src): Copies the src string into the dest array. Does not pad (if src already has values and dest is shorter, the values stay there after the null terminator). Make sure that dest is long enough, otherwise will not null-terminate.
- char *strcat(char *dest, char *src): Append the src string to dest str
- void *memset(void *ptr, int value, size_t num): Set the first num bytes at the location pointed by ptr to value.

## ctype.h
- Case manipulation:
    - int x = toupper(int c);
    - int x = tolower(int c);
- Char testing:
    - int x = isalpha(int c); // non-zero if true, 0 otherwise
    - int x = isalphanum(int c); // as above
    - int x = isdigit(int c); // as above
