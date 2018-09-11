# Dependency Injection

Item 5 of *Effectice Java*(3rd edition) is: **Prefer dependency injection to hardwiring resources**.

While dependency injection might sounds intimidating, it's actually very simple. One form of D.I. is **passing the resource into the constructor when creating a new instance**. 

You might wondering why. The simple answer is that it greatly improve the flexibility and testability of the code, because it decouples dependent classes.

Example from *Effective Java*:

```java
public class SpellChecker {
    private final Lexicon dictionary;
    
    public SpellChecker(Lexicon dictionary) {
        this.dictionary = Objects.requireNonNull(dictionary);
    }
    
    public boolean isValid(String word) { ... }
    
    public List<String> suggestions(String typo) { ... }
}
```

In this case, we inject `Lexicon` class object into SpellChecker so that we can easily mock an instance with expected Lexicon methods/properties in tests.

