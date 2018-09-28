# A Race Condition Example

The following is a rance condition/thread unsafe example in Java.

```java
public class TestJava {
    public static void main(String[] args) throws InterruptedException {
        ThreadSafeTest testClass = new ThreadSafeTest();

        Thread thread1 = new Thread() {
            @Override
            public void run() {
                testClass.test();
            }
        };

        Thread thread2 = new Thread() {
            @Override
            public void run() {
                testClass.test();
            }
        };

        thread1.start();
        thread2.start();

        thread1.join();
        thread2.join();
    }
}

class ThreadSafeTest {
    private int shared;

    void test() {
        for (int i = 0; i < 100000; i++) {
            int before = shared;
            shared++;
            int after = shared;
            if (before != after - 1) {
                System.out.println("Race condition found, before: " + before + " after: " + after);
            }
        }
    }
}
```

Note that we need to start thread1 and thread2 at about the same time.