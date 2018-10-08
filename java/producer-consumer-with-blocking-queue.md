# Producer-Consumer Pattern with Blocking Queue

*Java Concurrency in Practice* talks about blocking queue and producer-consumer pattern in chapter 5.3.

The example there is desktop search, with producer threads crawling the file system and consumer thread indexing the qulified files.

```java
public class FileCrawler implements Runnable {
    private final BlockingQueue<File> fileQueue;
    private final FileFilter fileFilter;
    private final File root;

    // constructors here
    
    public void run() {
        try {
            crawl(root);
        } catch (InterruptedException e) {
            Thread.currentThread().interrupt();
        }
    }
    
    private void crawl(File root) throws InterruptedException {
        // crawl and put to fileQueue
    }
}

public class Indexer implements Runnable {
    private final BlockingQueue<File> queue;
    
    public Indexer(BlockingQueue<File> queue) {
        this.queue = queue;
    }
    
    public void run() {
        try {
            while(true) {
                indexFile(queue.take());
            }
        } catch (InterruptedException e) {
            Thread.currentThread().interrupt();
        }
    }
}

public static desktopIndexing(File[] roots) {
    BlockingQueue<File> queue = new LinkedBlockingQueue<File>(BOUND);
    FileFilter filter = new FileFilter() {
        public boolean accept(File file) { return true; }
    }
    
    for(File root : roots)
        new Thread(new FileCrawler(queue, filter, root)).start();
    
    for(int i = 0; i < N_CONSUMERS; i++)
        new Thread(new Indexer(queue)).start();
}
```

BlockingQueue simplifies the implementation of producer-consumer pattern.

