# Java Exception

Java Exception hierachy.

![exception-hierarchy-in-java](exception-hierarchy-in-java.png)

From http://www.benchresources.net/exception-hierarchy-in-java/.

### Best practices:

- Use `try-with-resources` and multiple catch.
- When catching exception, be as specific as possible.
- Don't swollow exception.
- [printStackTrace](https://docs.oracle.com/javase/9/docs/api/java/lang/Throwable.html#printStackTrace) is not suitable in production environment because it use STERR, use logging framework instead.
- Throw early, catch late.

From performance perspective:

- Try-catch block has extra performance cost, it affects JVM code optimization. 
- Every Exception instance will cause a stack snapshot, which is an expensive operation. Frequent exceptions may affect service performance.

Questions:

- Difference between `NoClassDefFoundError` and `ClassNotFoundException`?
  - ClassNotFoundException is an exception when you try to load a class at run time using `Class.forName()` or `loadClass()` methods and class is not found in the classpath.
  - NoClassDefFoundError is an error occors when a class is present at compile time but not at run time.
- How to best handle exceptions in non-blocking, event driven or reactive programming pattern?

参考：

- 极客时间Java核心技术36讲
- https://dzone.com/articles/java-classnotfoundexception-vs-noclassdeffounderro

