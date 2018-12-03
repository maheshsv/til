# String, StringBuffer and StringBuilder

## String

- Immutable, final class, final attributes. Threadsafe,
- Constant pool, reuse.

## StringBuffer

- **Thread safe** string concatenation with **Synchronized**. Has performance cost.

## StringBuilder

- StringBuffer without synchironization, no performance cost. Recommend to use it when thread safe is not a concern, which is mostly true.



JDK 9 use byte array instead of char array to implement String.

