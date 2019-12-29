# Snowflake & Elastic Data Warehouse

* [The Snowflake Elastic Data Warehouse Paper](http://pages.cs.wisc.edu/~remzi/Classes/739/Spring2004/Papers/p215-dageville-snowflake.pdf).

* [The Snowflake Elastic Data Warehouse
SIGMOD 2016 and beyond](https://15721.courses.cs.cmu.edu/spring2018/slides/25-snowflake.pdf)

## Ideas

- build data warehouse in cloud era
- storage and computing layer separation and scale independently
- table files, hybrid columnar storage, tables horizontally partitioned into immutable micro-partitions
- matadata stored in a transactional key-value store
- vitural warehouse: EC2 worker nodes cluster as computing layer
- execution engine: columnar, vetorized, push down, etc
- Snapshot isolation, MVCC, versioned snapshots for time travel and cloning
- pruning to speed up data processing
