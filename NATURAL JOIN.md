**NATURAL JOIN**

In 'Natural Join' we don't need to specify the condition
it automatically locates the simller column and join bases of them.

```SQL
SELECT
    o.order_id,
    c.first_name,
FROM orders o
NATURAL JOIN customers c
```
NOTE :<b> not recommanded</b>
