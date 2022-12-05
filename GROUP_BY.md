**GROUP BY**

```SQL
SELECT
    SUM(invoice_total) AS total_sales
FROM invoices
GROUP BY client_id
```

```SQL
SELECT
    client_id,
    SUM(invoice_total) AS total_sales
FROM invoices
GROUP BY client_id
ORDER BY total_sales DESC
```

```SQL
SELECT
    client_id,
    SUM(invoice_total) AS total_sales
FROM invoices
GROUP BY client_id
WHERE invoice_date >= '2019-07-01'
ORDER BY total_sales DESC

```


```SQL
SELECT
    state,
    city,
    SUM(invoice_total) AS total_sales
FROM invoices i
JOIN clients
    USING (client_id)
GROUP BY state , city
```

```SQL
SELECT
    date,
    pm.name AS payment_method,
    SUM(amount) AS total_payments
FROM payments p
JOIN payment_methods pm
    ON p.payment_method = pm.payment_method_id
GROUP BY date , payment_method
ORDER BY date

```


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
GROUP BY
    c.customer_id,
    c.first_name,
    c.last_name
HAVING total_sales > 100
```
