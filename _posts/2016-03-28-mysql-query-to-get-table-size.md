---
title: A MySQL Query to Report on Table Size
tags: [MySQL]
description: A MySQL Query to Report on Table Size
---

A very useful query for getting the top tables in a MySQL datbase in terms of storage (GB) and row count.


```sql
SELECT CONCAT(table_schema, '.', table_name)					      table_name,
       CONCAT(ROUND(table_rows / 1000000, 2), 'M')                                    ROWS,
       CONCAT(ROUND(data_length / ( 1024 * 1024 * 1024 ), 2), 'G')                    DATA,
       CONCAT(ROUND(index_length / ( 1024 * 1024 * 1024 ), 2), 'G')                   idx,
       CONCAT(ROUND(( data_length + index_length ) / ( 1024 * 1024 * 1024 ), 2), 'G') total_size,
       ROUND(index_length / data_length, 2)                                           idxfrac
FROM   information_schema.TABLES
ORDER  BY data_length + index_length DESC
LIMIT  10;
```