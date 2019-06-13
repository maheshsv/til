# Rate Limiting Algorithms

### Common rate limiting algorithms

- [Token bucket](https://en.wikipedia.org/wiki/Token_bucket)
- Fixed window counter
- Sliding log
- Sliding window

[Here] is a good explanation of these algorithms.

---

### Use Guava to implement a rate limiter. 

The following example creates a rate limiter of 10 per second.

```java
import java.sql.Timestamp;

import com.google.common.util.concurrent.RateLimiter;

public class RateLimitTest {

    public static void main(String[] args) {
        RateLimiter rateLimiter = RateLimiter.create(10);
        while (true) {
            rateLimiter.acquire();
            Timestamp timestamp = new Timestamp(System.currentTimeMillis());
            System.out.println(timestamp + " accept.");
        }
    }

}
```
