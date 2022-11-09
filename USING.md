**USING**

instead of 'ON' we use USING
it simplify our Query  but we only 'USING' when the column name is same in both tables


```SQL
SELECT
    o.order_id
    c.first_name
FROM orders o
JOIN customers c
    --ON o.customer_id = c.customer_id
    USING(customer_id)
```

**using with multitable**

```SQL
SELECT
    o.order_id,
    c.first_name,
    sh.name AS shipper
FROM orders o
JOIN customers c
    USING(customer_id)
JOIN shippers sh
    USING(shipper_id)
```

**using with compsite key**
```SQL
SELECT *
FROM order_items oi
JOIN order_item_notes oin
    /* ON oi.order_id = oin.order_id
    AND oi.product_id = oin.product_i */
    USING(order_id,product_id)
```

```SQL
-- ex --
SELECT p.date , c.name ,p.amount  , pm.name as payment_method FROM payments p
JOIN clients c
	USING (client_id)
JOIN payment_methods pm
	ON payment_method = payment_method_id

```
