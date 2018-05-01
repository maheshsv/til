# Crash Course in Compilers

Note from [A crash course in compilers](https://increment.com/programming-languages/crash-course-in-compilers/).

Diving deeper into PLT(programming language theory) is a great way to grow as a developer.

> Turing completeness is the devisive factor to makes something a programming language.

And there are systems that are [accidentally Turing complete](http://beza1e1.tuxen.de/articles/accidentally_turing_complete.html).



Feed code into **compilers** or **interpreters**.



# How does a compiler work?

#### Parsing

- Lisp family: simple.
- Other languages more complex: scanning and parsing, Lex/Yacc.

#### Analysis

- Analyze the parsed code into **AST**.
- optimization
- type checking, etc

### Emission

- Emit target code
- machine code/LLVM IR(intermediate representation)
- Bytecode



### Tooling and Ecosystems

Very important for a language.

[Language Server Protocol](https://langserver.org/): make it easier to integrate new programming languages with text editors.

