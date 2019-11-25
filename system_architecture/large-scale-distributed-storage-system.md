# Large Scale Distributed Storage System

(Building a Large-scale Distributed Storage System Based on Raft)[https://www.cncf.io/blog/2019/11/04/building-a-large-scale-distributed-storage-system-based-on-raft/].

Two key points of designing a distributed storage system:
- sharding
- metadata storage

### Sharding

Pros and cons of:
- range-based sharding
- hash-based sharding

and hash-range combination sharding is also possible.

TiKV chose range-based sharding.

### Replication

Raft algorithm for data replication.

Multi-raft algorithm for large scale data store, each raft group for one region(range shard), split region once it gets too large(currently 96M), which happens on all physical nodes where the Region is located.

### Scheduling in a distributed storage system

Placement Driver(PD)
- routing table
- scheduler

PD stateless

epoch mechanism
