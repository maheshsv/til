# Redshift

[AWS Redshift](https://aws.amazon.com/redshift/) is a big data analytics solution for petabyte-scale data.

### System Architecture

![redshift-architecture](redshift-architecture.png)



### Key features

- Standard PostgreSQL interface
- MPP(Massive Parallel Processing)
- Columnar Data Storage



Standard PostgreSQL interface allows people to run queries with SQL, or use JDBC to connection. MPP enables many compute nodes to handle complex queries in parallel and result in fast processing speed. And columnar store is similar to other columnar system such as Big Query, it allows the engine to only fetch the necessary data and also easier data compression.



AWS have a good documentation about [how these features help Redshift to achieve exetremely fast query execution over huge amount of data](https://docs.aws.amazon.com/redshift/latest/dg/c_challenges_achieving_high_performance_queries.html).

