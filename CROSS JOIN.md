**CROSS JOIN**

The CROSS JOIN keyword returns all matching records from both tables whether the other table matches or not.
table1 records
id,name
1,a
2,b

table 2 records
id,class
1,x
2,xII

output:

a,x
a,xII
b,x
b,XII

```SQL
SELECT name , class
FROM table1
CROSS JOIN table2
ORDER BY name
```
```SQL
SELECT
    c.frist_name AS customer,
    p.name AS product
FROM customers c
CROSS JOIN products p
ORDER BY c.frist_name
```
**implecit syntax**
```SQL
SELECT
    c.frist_name AS customer,
    p.name AS product
FROM customers c , products p
ORDER BY c.first_name
```

NOTE:
If you add a WHERE clause (if table1 and table2 has a relationship), the CROSS JOIN will produce the same result as the INNER JOIN clause