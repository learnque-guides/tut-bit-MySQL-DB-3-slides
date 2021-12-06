# Natural join

A natural join is, well, supposed to be magically natural. This means that you tell MySQL what tables you want to join, and it figures out how to do it and gives you an INNER JOIN result set.

```sql
SELECT col_name1, col_name2
FROM table1 NATURAL JOIN table2;
```

It's not recommended to use it, because of magic :)