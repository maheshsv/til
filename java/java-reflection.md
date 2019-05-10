# Java Reflection: Call Methods at Runtime

## Call Methods at Runtime with Java Reflection

Notes from [here](https://www.baeldung.com/java-method-reflection).

```java
public class Operations {
    public double publicSum(int a, double b) {
        return a + b;
    }
 
    public static double publicStaticMultiply(float a, long b) {
        return a * b;
    }
 
    private boolean privateAnd(boolean a, boolean b) {
        return a && b;
    }
 
    protected int protectedMax(int a, int b) {
        return a > b ? a : b;
    }
}
```

### First, get Method object.

```java
Method sumInstanceMethod = Operations.class.getMethod("publicSum", int.class, double.class);

Method multiplyStaticMethod = Operations.class.getMethod("publicStaticMultiply", float.class, long.class);
```

> We can use `getDeclaredMethod()` to get any method defined in the class. This includes public, protected, default access, and even private methods but excludes inherited ones.

```java
Method andPrivateMethod = Operations.class.getDeclaredMethod("privateAnd", boolean.class, boolean.class);

Method maxProtectedMethod = Operations.class.getDeclaredMethod("protectedMax", int.class, int.class);
```

### Invoking Methods

> Call `invoke()` to execute the underlying method and get the returned object.

- instance methods: first argument must be in instance of method.

```java
@Test
public void givenObject_whenInvokePublicMethod_thenCorrect() {
    Method sumInstanceMethod
      = Operations.class.getMethod("publicSum", int.class, double.class);
 
    Operations operationsInstance = new Operations();
    Double result
      = (Double) sumInstanceMethod.invoke(operationsInstance, 1, 3);
 
    assertThat(result, equalTo(4.0));
}
```

- static methods: don't require an instance.

```java
@Test
public void givenObject_whenInvokeStaticMethod_thenCorrect() {
    Method multiplyStaticMethod
      = Operations.class.getDeclaredMethod(
        "publicStaticMultiply", float.class, long.class);
 
    Double result
      = (Double) multiplyStaticMethod.invoke(null, 3.5f, 2);
 
    assertThat(result, equalTo(7.0));
}
```

### Method accessibility

> By default, not all reflected methods are accessible. By calling `setAccesible(true)` on a reflected method object, the JVM suppresses the access control checks and allows us to invoke the method without throwing an exception.

```java
@Test
public void givenObject_whenInvokePrivateMethod_thenCorrect() {
    // ...
    andPrivateMethod.setAccessible(true);
    // ...
    Boolean result
      = (Boolean) andPrivateMethod.invoke(operationsInstance, true, false);
 
    assertFalse(result);
}
```
