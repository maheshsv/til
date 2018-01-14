# Alibaba Database Meetup

### Ali X-DB

**X-Paxos**

Paper: Paxos Made Live

Batching & Pipelining: improve throughput

Raft: receiver need to be in order

Asynchronization

**X-Engine: Storage Engine**

SW/HW co-design

Layered storage

High perf

Low storage cost

Paper:

- Shimin Chen SIGMOD2001 … through perfetching


- MassTree

Adaptive hot/cold data recognition & Anti-cache

Adaptive data encoding, compression and hybrid row-column stores

**Computation and Storage Decoupling**

- Based on Pangu shared storage
- On-demand storage extension
- Stateless computation nodes
- Best deployed in Cloud

**SQL Engine Enhancement**

Plan Cache

**Multi-version Schema & Fast DDL**

He Dengcheng 何登成

---

### Cloud SQL: MySQL & PostgreSQL, PD as the block device

Compute Engine VM => Persistent disk

**Cloud Storage:**

Persistent Disk(PD):

- Network-attached block device
- Log structured volume(LSV)

3 copies: optimize read/write latency

Blocks are stored along with metadata:

- Self-describing
- Check integrity

Snapshots of data block

PD benefits: Live Migration

**网络快存储**

---

### RocksDB

**Versatile**

- Diversified application
- Diversified workloads

### Use case

- Document Store
- Social graph edges
- Time-ordered events
- Counter service
- Storage for logs
- RocksDB as Cache

**LSMT: log structure merge tree**

Leveled compaction

MyRocks = MySQL + RocksDB Engine

**Space Efficiency**

Random updates using B-tree: not efficient

---

### Alibaba OLAP

Key tech:

- Hybrid storage
- Mixed workload
- optimizer
- MPP + DAG
- Adaptive compression
- GPU/FPGA acceleration

flyinweb

