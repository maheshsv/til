# Bloom Filter

A bloom filter is a fast and meory efficient data structure to test if an element is in a set.

### Algorithm description

1. create a bit array
2. have some hash functions
3. for given data, run the hash functions on the data and set the bits at the hash result positions to 1.
4. to test if an element is in a set, hash the element and check if the hash result positions are 1. If no, we are **sure** it's not in the set, if yes, then there is a possibility that the element is in the set.

There is a good tutorial of bloom filter [here](https://llimllib.github.io/bloomfilter-tutorial/). And [Bloom Filter in Java using Guava](https://www.baeldung.com/guava-bloom-filter).
