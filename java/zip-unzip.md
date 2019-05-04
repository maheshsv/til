# Zip and Unzip

Zip archive in Java notes from [Core Java](https://www.amazon.com/Core-Java-II-Advanced-Features-11th/dp/0135166314) and [Zipping and Unzipping in Java](https://www.baeldung.com/java-compress-and-uncompress).

Example code to zip and unzip files.

```java
import java.io.*;
import java.util.Arrays;
import java.util.List;
import java.util.zip.ZipEntry;
import java.util.zip.ZipInputStream;
import java.util.zip.ZipOutputStream;

public class ZipArchive {

    public static void main(String[] args) throws IOException {
        zipFiles();
        unzipFiles();
    }

    private static void zipFiles() throws IOException {
        List<String> files = Arrays.asList("a.txt", "b.txt");
        FileOutputStream fos = new FileOutputStream("c.zip");
        ZipOutputStream zos = new ZipOutputStream(fos);
        for (String fileName : files) {
            File file = new File(fileName);
            FileInputStream fis = new FileInputStream(file);
            ZipEntry zipEntry = new ZipEntry(file.getName());
            zos.putNextEntry(zipEntry);

            byte[] bytes = new byte[1024];
            int length;
            while ((length = fis.read(bytes)) >= 0) {
                zos.write(bytes, 0, length);
            }
            fis.close();
        }
        zos.close();
        fos.close();
    }

    private static void unzipFiles() throws IOException {
        String zipFileName = "c.zip";
        File zipFile = new File(zipFileName);
        ZipInputStream zis = new ZipInputStream(new FileInputStream(zipFile));

        ZipEntry zipEntry = zis.getNextEntry();
        while (zipEntry != null) {
            System.out.println(zipEntry.getName());
            // todo: save entry content to file.
            zipEntry = zis.getNextEntry();
        }
        zis.closeEntry();
        zis.close();
    }
}
```
