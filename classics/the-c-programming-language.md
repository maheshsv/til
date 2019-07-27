# The C Programming Language

Notes from the classic C bible: [K & R](https://www.amazon.com/Programming-Language-2nd-Brian-Kernighan/dp/0131103628).

### Types, Operators, Expressions

- variable
- basic data types:
    - char
    - int
    - float
    - double
- constants, enum
- type conversions

### Control Flow

The control flow of C is very similar to other C family languages, it also has `goto` and labels.

### Functions and Program Structure

- Basics of functions
- External variables: defined outside of any function
- header files
- static variables:
    - apply to external variables, limit the scope to the file.
    - apply to internal variables, make variables permanent within a single function.
- register variables
- preprocessor
    - file inclusion: `#include "filename"` or `#include <filename>`.
    - Macro substitution: `#define name replacement-text`.
    - conditional inclusion: `#if #elif ... #else #endif`, `#ifndef #define #endif`.

### Pointers and Arrays

**A pointer is a variable that contains the address of a variable**.

- pointers and arrays
- address arithmetic
- character pointers
- pointer arrays, pointers to pointers
- command-line arguments
- pointers to functions: e.g: `int (*comp)(void *, void *)`.
- complicated declarations

### Structures

- pointers to structures: e.g: `struct key *binsearch`.
- self-referential structures
- typedef: e.g: `typedef struct tnode *Treeptr` creates a new type called `Treeptr`.
- Unions: a variable that may hold objects of different types and sizes

### Input and Output

Input and output facilities are not part of the C language itself.

- Standard input and output
- Formatted output: printf
- variable-length argument lists
- Formatted input: scanf
- File access
- Error handling: stderr and exit
- Line input and output

### Unix System Interface

- File descriptors
- Low level I/O: read and write
- Open, create, close, unlink
- Random access: lseek
