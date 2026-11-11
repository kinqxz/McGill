# COMP 206 — Lecture 12

**Course:** Introduction to Software Systems  
**Date:** October 15th 2026
**Topic:** Data and Control Structures in C

---
## Basic data types
- char: represented as an integer. Must be smallest addressable unit of memory: Usually 8 bits. Values depend on the machine's character set
- int: Integer (whole number). C specifies that int must be at least 16 bits (-32,768 to 32,767), but on 32-bits and 64-bits machines it is usually 32 bits (-2,147,483,648 to 2,147,483,647)
- float: Floating-point number (i.e. can have a fractional part). Usually 32 bits. Ranges about 1.18*10^-38 to 3.40*10^38 with 6 digits precision
- double: Floaintg point number that is double the size of float.

There are some type modifiers that you can add in front of some of these types:
- You can add signed or unsigned in front of char and int
    - Signed numbers can represent positive or negative nums, while unsigned only non-negative.
    - without this modifier, int is signed and char might be either.
- You can add short or long in fron of int

You can see the size of a type by doing **sizeof()**.

## Derived data types
- Arrays: Combine items with the same type
- Structures: Combine items with different types
- Pointer: Address to an object in memory
- Unions: Combine items with different types butt holding only one value at a time.

Strings do not have a type, they are either char * (an address to a character) or char[] (an array of characters)


## Constant

``` C
int const A = 1;
const int A = 2; // either works
```

## typedef Declaration
typedef command allows for the creation of custom type names. This makes the program mroe readable, and will be particularly useful with derived data types (e.g. structs)

``` C
typedef int age;
int main() {
    age alice, bob;
    alice = 27;
    bob = 32;
    printf("Alice is %d years old\n", alice);
    printf("Bob is %d years old\n", bob);
}
```

## Pre vs post increment/decrement

Var++ -> increment after solving the expression

++Var -> increameent before sovling the expression

Same applies for decrementing

## Logical operators 
All same as java

Also, x = 5 > 10;, will result in 1 for true, or 0 for false.

## Control structures

### If-statement
if (CONDITION) SINGLE_STATEMENT;

if (CONDITION) {MULTIPLE_STATEMENTS;}

if (CONDITION) {STATEMENTS;}
else if {STATEMENTS;}
else {STATEMENTS;}

0 is false, and everything else prints.

## Ternary operator
Also called conditional operator. shorthand for simple if-statements

Syntax:
``` C
(condition) ? true_expression : false_expression;
var = (condition) ? true_expression : false_expression;
```

## Switch-statement
switch(EXPRESSION) {
    case VALUE: MULTIPLE STATEMENTS;
    break;

    case VALUE2: MULTIPLE_STATEMENTS;
    break;
    default:
        MULTIPLE STATEMENTS;
}

EXPRESSION must evaluate to an integer (or character)

If there is no break statement, execution automatically goes to the next case block without testing the condition.

## While loop
while (CONDITION_IS_TRUE) SINGLE_STATEMENT;

while (CONDITION_IS_TRUE) {MULTIPLE_STATEMENTS;}

## Do-while loop
Similar to while loop, but condition is evaluated after running block. It always at least runs once!

## For loop
The INIT expression is run before the loop starts

the CONDITION expression is checked before each iteration, and the loop runs as long as it evaluates to true

the ITERATION expression is run after each iteration

for (INIT; CONDITION; ITERATION) SINGLE_STATEMENT;

for (INIT; CONDITION; ITERATION) {MULTIPLE_STATEMENTS};

You can do this for example:
``` C
int x, y;
for (x=0, y=10; x*y<45; x+=2, y--) {
    puts("Hi");
}

