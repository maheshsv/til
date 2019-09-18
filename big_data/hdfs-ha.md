# HDFS High Availability

HDFS was build based on Google File System paper. And prior to hadoop 2.0, the NameNode was a single point of failure. So how does HDFS 2.0 achieved high availability?

It's actually explained in [hadoop documentation](https://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/HDFSHighAvailabilityWithNFS.html). Basically there are 2 options: use shared storage or quorum journal manager.

### Using shared storage

The active NameNode and slave NameNode share some storage device, e.g an NFS. The log of edit operations in active NameNode are recorded in the shared storage device and the slave can read the log and update itself.

### Using quorum journal manager

This is similar to Paxos/Raft algorithm. Both active and slave nodes talk to "JournalNodes", there are at least 3 JNs. The active node log modifications to a majority of the JNs, and slave node reads from the log and applies the changes to itself.
