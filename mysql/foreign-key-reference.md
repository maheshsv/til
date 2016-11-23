# Find foreign key reference information

From [StackOverflow](http://stackoverflow.com/questions/806989/mysql-how-to-i-find-all-tables-that-have-foreign-keys-that-reference-particular).

To find all of the tables with foreign key to a specific table/column:

```
USE information_schema;
SELECT *
FROM
  KEY_COLUMN_USAGE
WHERE
  REFERENCED_TABLE_NAME = 'X'
  AND REFERENCED_COLUMN_NAME = 'X_id';
```

`INFORMATION_SCHEMA` database stores the metadata of other MySQL databases. For reference, check [here](http://dev.mysql.com/doc/refman/5.7/en/information-schema.html).
