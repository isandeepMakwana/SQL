**UNION**

it used for combine 2 and more Queries

```SQL
SELECT
    order_id,
    order_date,
    'Active' AS status
FROM orders
WHERE order_date >= '2019-01-01'

UNION

SELECT
    order_id,
    order_date,
    'Archived' AS status
FROM orders
WHERE order_date < '2019-01-01';
```

```SQL
SELECT first_name,
FROM archived_orders
UNION
SELECT name
FROM orders
```

--ex--
```SQL
SELECT c.customer_id , c.first_name , c.points, 'GOLD' AS type
FROM customers c WHERE c.points > 3000
UNION
SELECT c.customer_id , c.first_name , c.points, 'Silver'
FROM customers c WHERE c.points BETWEEN 2000 AND 3000
UNION
SELECT c.customer_id ,c.first_name, c.points,'Bronze'
FROM customers c WHERE c.points < 2000
ORDER BY first_name
```