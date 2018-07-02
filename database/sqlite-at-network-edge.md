# SQLite: The Database at the Edge of the Network

The video is available [here](https://www.youtube.com/watch?v=Jib2AmRb_rk).

> SQLite is the database at the edge of the network. It doesn't compete with MySQL, PostgreSQL etc. It competes with `fopen()`!

#### storage decision checklist

- remote data

- big data
- concurrent writers

Otherwise => SQLite



Side note: Dr. Richard Hipp and the SQLite team spent huge efforts on the tests of SQLite. And the tests really define how SQLite supposed to work, and it enables them to do any kind of refactoring of the system or sub-system. The TiDB team also emphasized the importance of tests for TiDB to be successful.

