**HAVING**

```SQL
SELECT
    client_id,
    SUM(invoice_total) AS total_sales
FROM invoices
GROUP BY client_id
HAVING total_sales > 500

```


```SQL
SELECT
    client_id,
    SUM(invoice_total) AS total_sales
    COUNT(*) AS number_of_invoices
FROM invoices
GROUP BY client_id
HAVING total_sales > 500 AND number_of_invoices > 5
```

--ex--
> Get the customers
>       located in Virginia
>       who have spent more then $100

```SQL
SELECT
    c.customer_id,
    c.first_name,
    c.lastname,
    SUM(oi.quantity*oi.unit_price) AS total_sales
FROM cusotmer c
JOIN order o
    USING (customer_id)
JOIN order_items oi USING (order_id)
WHERE state = 'VA'
GROUP BY -- all the select column needed to use in Group by
    c.customer_id,
    c.first_name,
    c.last_name
HAVING total_sales > 100
```
