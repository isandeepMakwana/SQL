**NATURAL JOIN**

In 'Natural Join' do not want to specify the situation
it automatically locates the simller column and join bases of them.

```SQL
SELECT
    o.order_id,
    c.first_name,
FROM orders o
NATURAL JOIN customers c
```
NOTE :<b> not recommanded</b>
