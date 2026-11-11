# COMP 206 — Lecture 15

**Course:** Introduction to Software Systems  
**Date:** October 27th 2026
**Topic:** Strings, Functions, More Standard Utilities

---
# C Functions
Syntax:

RETURN_TYPE FN_NAME(PARAMETERS){
    BODY;
    return EXPRESSION;
}

Where:
- RETURN_TYPE: the type of value returned by the function, void can be used too mean nothing will be returned, cannot be an array.
- FN_NAME: function's name, must be unique
- PARAMETERS: a comma seperated list like TYPE1 VAR1, TYPE2 VAR2, etc.
    - void if the function takes no parameter
- BODY: C code.
- return EXPRESSION: Specifies what value will be returned. EXPRESSION is often a variable or contrant but could be arithmetic or ternary operator etc. Must agree with RETURN_TYPE, if void return type, can ignore or write return;, A function can have multiple return statements to return early (for example in an if statement)

Ex:
``` C
int sum(int a, int b) {
    int c;
    c = a + b;
    return c;
}
```

C is a 1-pass compiler

## Function prototype
Functions need to be declared before use so that the compilers knows the expected arguments and return type, but they don't need to be defined

A function declaration that doesn't have a body is called a function prototype