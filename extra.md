```SQL
select
    order_id,
    order_date,
    'ACTIVE' AS status
FROM orders
WHERE order_date >= '2019-01-01';
```
