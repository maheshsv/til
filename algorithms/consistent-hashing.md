# Consistent Hashing

> Consistent Hashing is a special kind of hashing such that when a hash table resized, only K/n keys need to be remapped on average, where K is the number of keys, and n is the number of slots.

### Usage in distributed systems

- Hash nodes and keys to a number range, represented in a circle
- When a node added or removed, only migrate the keys in the range that the node is responsible for

There is a good explanations and implementations in Java [here](http://www.tom-e-white.com/2007/11/consistent-hashing.html).

### Implementation in Python from [here](http://techspot.zzzeek.org/2012/07/07/the-absolutely-simplest-consistent-hashing-example/). 

```python
import bisect
import md5

class ConsistentHashingRing(object):
    def __init__(self, replicas=100):
        self.replicas = replicas
        self._keys = []
        self._nodes = {}

    def _hash(self, key):
        return long(md5.md5(key).hexdigest(), 16)

    def _repl_iterator(self, nodename):
        return (self._hash("%s:%s" % (nodename, i)) for i in xrange(self.replicas))

    def __setitem__(self, nodename, node):
        for hash_ in self._repl_iterator(nodename):
            self._nodes[hash_] = node
            bisect.insort(self._keys, hash_)

    def __delitem__(self, nodename):
        for hash_ in self._repl_iterator(nodename):
            del self._nodes[hash_]
            index = bisect.bisect_left(self._keys, hash_)
            del self._keys[index]

    def __getitem__(self, key):
        hash_ = self._hash(key)
        start = bisect.bisect(self._keys, hash_)
        if start == len(self._keys):
            start = 0
        return self._nodes[self._keys[start]]

cr = ConsistentHashingRing(2)

cr["node1"] = "host1"
cr["node2"] = "host2"
print cr.__dict__

client = cr["some key"]
print client

```

Output

```bash
{'_nodes': {234270789901673706184978332503042424895L: 'host2', 30800198962622170283128992779263460808L: 'host2', 127097526815233298582794356773614554855L: 'host1', 82085472036366309913032597666696857451L: 'host1'}, '_keys': [30800198962622170283128992779263460808L, 82085472036366309913032597666696857451L, 127097526815233298582794356773614554855L, 234270789901673706184978332503042424895L], 'replicas': 2}
host2
```



`Replicas` is the number of "virtual nodes" each node has. `_nodes` stores the number range checkpoints to node mapping. `_keys` is a sorted list of the number range checkpoints. Therefore, we can use binary search to find the key in log(n) time, otherwise we need to check all of the keys in the dictionary to find the node.

