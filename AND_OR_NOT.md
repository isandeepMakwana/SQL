**AND , OR , NOT**
```SQL
-- AND execute 1st (*)
-- OR execute 2nd (+)
/* always use ( ) */

SELECT * FROM customers WHERE birth_date > '1990-01-01' OR ( points > 1000 AND state= 'VA')
```

```SQL
SELECT * FROM order_items WHERE order_id=6 AND unit_price * quantity > 30 -- you can use arthmatic operation after Where clause;
```
