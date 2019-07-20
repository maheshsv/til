# Log Structured Merge Tree

Note from [Designing Data-Intensive Applications](https://www.amazon.com/Designing-Data-Intensive-Applications-Reliable-Maintainable/dp/1449373321).

Log Structured Merge Tree, aka LSM-Tree and B-Tree are 2 of the most popular data structures powering database index.

## LSM-Tree

The algorithm of LSM-Tree:

### Write

- Write first goes into in-memory balanced tree, called memtable. And keep a separate append only log to track the writes for crash recovery.
- When the memtable size exceeds a threshold, persist it to disk as an SSTable. And writes goes into a new memtable.
- From time to time, run a merging and compaction of segments process in the background.

### Read

- First try to look up the key in the memtable, if not found, go to the most recent SSTable on the disk, and then the next-oldest SSTable, so on and so forth.
