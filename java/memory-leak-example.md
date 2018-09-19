# A Memory Leak Example

The following is a memory leak example from *Effective Java*.

```java
public class Stack {
    private Object[] elements;
    private int size = 0;
    private static final int DEFAULT_INITIAL_CAPACITY = 16;
    
    public Stack() {
        elements = new Object[DEFAULT_INITIAL_CAPACITY];
    }
    
    public void push(Object e) {
        ensureCapacity();
        elements[size++] = e;
    }
    
    public Object pop() {
        if(size == 0)
            throw new EmptyStackException();
        return elements[--size];
    }
    
    private void ensureCapacity() {
        if(elements.length == size) {
            elements = Arrays.copyOf(elements, 2 * size + 1);
        }
    }
}
```

The memory leak here is that in `pop` the elements get popped will not be garbage collected, because the Stack maintains ***Obsolete References*** to these objects.

The fix is to eliminate obsolete reference in `pop` method:

```java
elements[size] = null;
```

