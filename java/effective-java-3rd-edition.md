# Effective Java 3rd Edition

## General Principles

- Clarity and simplicity are of paramount importance.
- Components should be as small as possible but not smaller.
- Code should be reused rather than copied.
- Dependency between components should be kept to a minimum.
- Error should be detected ASAP, ideally at compile time.

Four kinds of types:

- interfaces(including annotations)
- classes(including enums)
- arrays
- primitives

A class's members consists of:

- fields
- methods
- member classes
- member interfaces

## Creating and Destroying Objects

### Item 1: Consider static factory methods instead of constructors

Examples:

```java
public static Boolean valueOf(boolean b) {
    return b ? Boolean.TRUE : Boolean.FALSE;
}

// from
Date d = Data.from(instant);

// of
Set<Rank> faceCards = EnumSet.of(JACK, QUEEN, KING);

// valueOf
BigInteger prime = BigInteger.valueOf(Integer.MAX_VALUE);

// instance/getInstance
StackWalker luke = StackWalker.getInstance(options);

// create/newInstance
Object newArray = Array.newInstance(classObject, arrayLen);

// getType
FileStore fs = Files.getFileStore(path);

// newType
BufferedReader br = Files.newBufferedReader(path);

// type
List<Complaint> litany = Collections.list(legacyLitany);
```

### Item 2: Consider a builder when faced with many constructor parameters

See builder pattern example code [here](builder-pattern.md).

The more interesting part now is using builder pattern for class hierarchies.

Example:

```java
public abstract class Pizza {
    public enum Topping { HAM, MUSHROOM, ONION, PEPPER, SAUSAGE };

    final Set<Topping> toppings;

    abstract static class Builder<T extends Builder<T>> {
        EnumSet<Topping> toppings = EnumSet.noneOf(Topping.class);
        public T addTopping(Topping topping) {
            toppings.add(Objects.requireNonNull(topping));
            return self();
        }

        abstract Pizza build();

        // Subclasses must override this method to return "this"
        protected abstract T self();
    }

    Pizza(Builder<?> builder) {
        toppings = builder.toppings.clone();
    }
}

```
