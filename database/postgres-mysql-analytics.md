# Compare Postgres and MySQL for Analytics

Why Postgres is better than MySQL for analytics. From [here](https://medium.com/holistics-software/why-you-should-use-postgres-over-mysql-for-analytics-purpose-e3df42df35d7)

### Postgres support CTE

WITH queries define temporary tables exist just for the query. Example:

```sql
WITH regional_sales AS (
        SELECT region, SUM(amount) AS total_sales
        FROM orders
        GROUP BY region
     ), top_regions AS (
        SELECT region
        FROM regional_sales
        WHERE total_sales > (SELECT SUM(total_sales)/10 FROM regional_sales)
     )
SELECT region,
       product,
       SUM(quantity) AS product_units,
       SUM(amount) AS product_sales
FROM orders
WHERE region IN (SELECT region FROM top_regions)
GROUP BY region, product;
```

### Postgres support window functions

Window functions is very useful when it comes to doing analytics.

### Postgres support schema(namespace)

Data pulled from different sources can be categorized to different namespaces.

### Postgres has bettern interface when dealing with datatimes

In Postgres:

```sql
DATE_TRUNC(ts, ‘DAY’)
DATE_TRUNC(ts, ‘WEEK’)
DATE_TRUNC(ts, ‘MONTH’)
```

In MySQL:

```sql
DATE(ts)
DATE_ADD(ts, INTERVAL (1-DAYOFWEEK(ts) DAY))
DATE_FORMAT(ts,’%Y-%m-01')
```

### Other small things:

- MySQL doesn’t support full outer join
- Wrong group by doesn’t throw error in MySQL
- Postgres supports VALUES for manual values list

```
# Postgres
values
  ('2015-01-01', 100, 200),
  ('2015-01-02', 200, 400),
  ('2015-01-03', 300, 600)
# MySQL
select '2015-01-01', 100, 200 union all
select '2015-01-02', 200, 400 union all
select 2015-01-03', 300, 600
```

- Postgres has generate_series
- Postgres has materialized views
