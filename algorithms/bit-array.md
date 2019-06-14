# Bit Array

### Advantages

- compact
- fast

### Disadvantages

- wasteful for sparse sets
- no native support from some languages

### Implementation in Java

The following `BitArray` class is excerpted from [Find Duplicates using bit array](https://www.geeksforgeeks.org/find-duplicates-of-array-using-bit-array/).

```java
public class BitArray {

    private int[] arr;

    public BitArray(int n) {
        // we need n/32 + 1 integers to store n bits.
        arr = new int[(n >> 5) + 1];
    }

    boolean get(int pos) {
        int index = pos >> 5;
        int bitNo = pos & 0x1F;

        return (arr[index] & (1 << bitNo)) != 0;
    }

    void set(int pos) {
        int index = pos >> 5;

        int bitNo = pos & 0x1F;
        arr[index] |= 1 << bitNo;
    }

    public static void main(String[] args) {
        int[] arr = {1, 5, 1, 10, 12, 10};

        BitArray bitArray = new BitArray(1000);
        for (int i : arr) {
            if (bitArray.get(i)) {
                System.out.println(i + " ");
            } else {
                bitArray.set(i);
            }
        }
    }
}
```
