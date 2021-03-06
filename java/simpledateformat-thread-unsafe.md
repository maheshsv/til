# SimpleDateFormat Not Thread Safe Example

Example code to show that `SimpleDateFormatter` is not thread safe tweaked from [here](https://www.callicoder.com/java-simpledateformat-thread-safety-issues/).

```java
import java.text.ParseException;
import java.text.SimpleDateFormat;
import java.util.Date;
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;

public class SimpleDateFormatterTest {

    private static SimpleDateFormat simpleDateFormat = new SimpleDateFormat("yyyy-MM-dd'T'HH:mm:ss");

    public static void main(String[] args) {
        String dateStr = "2018-06-22T10:00:00";

        ExecutorService executorService = Executors.newFixedThreadPool(2);
        Runnable task = () -> parseDate(dateStr);

        for (int i = 0; i < 100; i++) {
            executorService.submit(task);
        }

        executorService.shutdown();
    }

    private static void parseDate(String dateStr) {
        try {
            Date date = simpleDateFormat.parse(dateStr);
            System.out.println("Successfully Parsed Date " + date);
        } catch (ParseException e) {
            System.out.println("ParseError " + e.getMessage());
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```
