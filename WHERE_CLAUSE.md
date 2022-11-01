**Where clause**

```SQL
-- operation with date
SELECT * FROM customers WHERE birth_date > ' 1990-01-01 ';

SELECT count(*) FROM orders WHERE order_date >= ' 2019-01-01 ';
```