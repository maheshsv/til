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

---

## Code Snippets

Parse command-line args:

```c
#include <stdio.h>

int main(int argc, char *argv[]) {

    while (--argc > 0) {
        printf("%c\n", (*++argv)[0]);
        printf("%c\n", *++argv[0]);
    }

    return 0;
}
```

Pointer to function:

```c
void qsort(void *v[], int left, int right, int (*comp)(void *, void *)) {
    int i, last;

    void swap(void *v[], int, int);

    if (left >= right)
        return;
    swap(v, left, (left + right) / 2);
    last = left;
    for (i = left+1; i <= right; i++) {
        if ((*comp)(v[i], v[left]) < 0)
            swap(v, ++last, i);
    }
    swap(v, left, last);
    qsort(v, left, last - 1, comp);
    qsort(v, last + 1, right, comp);
}
```

Define pointer to function type:

```c
typedef int (*PFI)(char *, char *); // define pointer to function of two `char *` arguments and return `int` type `PFI`.
PFI strcmp, numcmp;
```

Formatted input: `Scanf`:

```c
// sample input: 25 Dec 1988
int day, year;
char monthname[20];

scanf("%d %s %d", &day, monthname, &year);
```

Loop and free items:

```c
for(p = head; p != NULL; p = p->next) // use pointer after it has been freed is ***WRONG***
    free(p);

// The right way:
for(p = head; p != NULL; p = q) {
    q = p->next;
    free(p);
}
```

Generate random floating-point number >= 0 and < 1:

```c
#define frand() ((double) rand() / (RAND_MAX+1.0))
```

Copy input to output with Unix interface:

```c
#include "syscall.h"

main() {
    char buf[BUFSIZ];
    int n;

    while((n = read(0, buf, BUFSIZ)) > 0)
        write(1, buf, n);
    return 0;
}
```
