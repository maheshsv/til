# SOLID Principles

SOLID principles from [wikipedia](https://en.wikipedia.org/wiki/SOLID_(object-oriented_design)).

### Single Responsibility Principle

a module/class should have only a single responsibility.

### Open/Close Principle

Software entities should be open for extension but closed for modification.

### Liskov Substitution Principle

Objects in a program should be replaceable with instances of their subtypes without altering the correctness of that program???

### Interface Segregation Principle

many client-specific interfaces are better than one general-purpose interface.

### Dependency Inversion Principle

one should “depend upon abstractions, [not] concretions."

---

The most confusing one for me is LSP, and there are some good explanation on [StackOverflow](https://stackoverflow.com/questions/56860/what-is-an-example-of-the-liskov-substitution-principle). In summary, LSP is about designing **correct abstraction**. For example, square is rectangle, but implement square class by inheriting from rectangle may violate LSP because square have the same width and height but rectangle doesn't.

There are quite a lot of good SOLID principles posts out there on the web, and [here](https://lostechies.com/derickbailey/2009/02/11/solid-development-principles-in-motivational-pictures/) is one.
