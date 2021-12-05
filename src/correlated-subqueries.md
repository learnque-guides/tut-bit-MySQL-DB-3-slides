# Correlated subqueries

Cannot be run independently.

```sql
SELECT custid, orderid, orderdate, empid
FROM Orders AS O1
WHERE orderid =
  (
    SELECT MAX(O2.orderid)
    FROM Orders AS O2
    WHERE O2.custid = O1.custid
  );
```

Will find latest orderid for current customer.

We can also use subqueries for calculating percentage of some value. Let's investigate such example:

```sql
SELECT orderid, custid, val,
  CAST(100. * val / (SELECT SUM(O2.val)
                     FROM OrderValues AS O2
                     WHERE O2.custid = O1.custid)
       AS DECIMAL(5,2)) AS pct
FROM OrderValues AS O1
ORDER BY custid, orderid;
```

SQL supports EXISTS predicate that can be used with subquries.

Lets' find orders that was not completed for customer

```sql
SELECT custid, companyname
FROM Customers AS C
WHERE country = 'Spain'
  AND NOT EXISTS
    (SELECT * FROM Orders AS O
     WHERE O.custid = C.custid);
```
Quiz:
* How we can achieve the same result with joins?
* How to find previous orderid for every order in Orders table (advanced)?