# Static Block

An example code snippet using static block:

```java
public class StaticBlockTest {

    static {
        System.out.println(StaticBlockTest.a);
    }

    private static String a = "hello";

    public static void main(String[] args) {
        System.out.println("In main.");
    }
}
```

The output is:

```bash
null
In main.
```


`StaticBlockTest.a` is null although it's assigned to be `hello`. To get this value in the static block, the static block needs to be after the assignment. Like the following:

```java
public class StaticBlockTest {

    private static String a = "hello";

    static {
        System.out.println(StaticBlockTest.a);
    }

    public static void main(String[] args) {
        System.out.println("In main.");
    }
}
```

In this case, the output is:

```bash
hello
In main.
```

And note that it's still executed before main.
