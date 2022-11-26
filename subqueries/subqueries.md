**subqueries**

```SQL
-- Find products that are more
-- expensive than lettuce (id =3)

SELECT *
FROM products
WHERE unit_price > (
    SELECT unit_price
    FROM products
    WHERE product_id =3
)
```

```SQL

-- Find employees whose earn more than average

SELECT *
FROM employees
WHERE salary > (
    SELECT AVG(salary)
    FROM employees
)
```

**IN**

-- Find the products that have never been ordered
```SQL
USE sql_store;

SELECT * products WHERE product_id NOT IN(
    SELECT DISTINCT product_id
    FROM order_items
)

```
```SQL
-- Find clients without invoices
USE sql_invoicing;

SELECT *
FROM clients
WHERE client_id NOT IN (
    SELECT DISTINCT client_id
    FROM invoices
)

-- or with join
SELECT * FROM clients
LEFT JOIN invoices USIGN(client_id)
WHERE invoice_id IS NULL

```

---

```SQL
use sql_store;
SELECT customer_id , first_name , last_name FROM customers WHERE customer_id IN (
select customer_id FROM orders WHERE order_id in(
SELECT order_id FROM order_items WHERE product_id =3
)
);

            or

SELECT DISTINCT c.customer_id , c.first_name , c.last_name FROM customers c
JOIN orders o
	ON  o.customer_id = c.customer_id
JOIN order_items ot
	ON ot.order_id = o.order_id
WHERE ot.product_id = 3;


```



```SQL
-- Find customers who have ordered lettuce (id =3)
--     select customer_id , first_name , last_name

USE sql_store;

SELECT *
FROM customers
WHERE customer_id IN (
    SELECT o.customer_id
    FROM order_items oi
    JOIN orders o USING (order_id)
    WHERE product_id = 3
);

-- OR with JOIN

SELECT DISTINCT customer_id , first_name , last_name
FROM customers c
JOIN orders o USING (customer_id)
JOIN order_items oi USING (order_id)
WHERE oi.product_id = 3;
```


```SQL
-- Select invoices larger than all invoices of
-- client 3

USE sql_invoicing;

SELECT *
FROM invoices
WHERE invoice_total > (
    SELECT MAX(invoice_total)
    FROM invoices
    WHERE client_id = 3
);
```
```SQL
-- Select clients with at least two invoices
SELECT *
FROM clients
WHERE client_id IN (
    SELECT client_id
    FROM invoices
    GROUP BY client_id
    HAVING COUNT(*) >= 2
)
```

---
---
> ALL

```SQL
-- Select invoices larger than all invoices of
-- client 3
SELECT * invoices
WHERE invoice_total > ALL(
    SELECT invoice_total
    FROM invoice_total
    WHERE client_id = 3
)

-- SELECT * FROM invoices
-- WHERE invoice_total > ALL (150,130,167,....)
```

> SOME

```SQL
-- any value is higher then this values

SELECT * invoices
WHERE invoice_total > SOME (150,130,167,....)
```

> ANY

```SQL
-- Select clients with at least two invoices
-- '=Any' => 'IN'
SELECT *
FROM clients
WHERE client_id = ANY (  -- (=ANY)   =>( IN )
    SELECT client_id
    FROM invoices
    GROUP BY client_id
    HAVING COUNT(*) >= 2
)
```


---

**Correlated subqueries**

```SQL
-- for each employee
--      calculate the avg salary for employee.office
--      return the employee if salary > avg

SELECT *
FROM employees e
WHERE salary > (
    SELECT AVG(salary)
    FROM employees
    WHERE office_id = e.office_id
);

```

**IN subqueries vs correlated subqueries**
> IN subqueries :-  first we calculated the inner queries then calculate outerquies

> correlated subqueries :- we calculated inner and outer queries symentensly

```SQL
-- Select client that have an invoice
SELECT *
FROM clients
WHERE client_id IN (
    SELECT DISTINCT client_id
    FROM invoices
)
```

> EXISTS
>
```SQL
SELECT *
FROM clients c
WHERE EXISTS (
    SELECT client_id
    FROM invoices
    WHERE client_id = c.client_id
)
```

-- EX --
```SQL
-- Find the products that have never been ordered
SELECT *
FROM products
WHERE product_id NOT IN (
    SELECT product_id
    FROM order_items
)
-- or using exists

SELECT *
FROM products p
WHERE NOT EXISTS (
    SELECT product_id
    FROM order items
    WHERE product id = p.product id
)

```

**Subqueries in the SELECT Clause**

```SQL
SELECT
    invoice_id,
    invoice_total,
    (SELECT AVG(invoice_total) FROM invoices) AS invoice_average,
    invoice_total - (SELECT invoice_average) AS difference,
FROM invoices

-- if we want to use invoice_average we need to write (SELECT invoice_average)

```

```SQL
SELECT
    client_id,
    name,
    (SELECT SUM(invoice_total) FROM invoices WHERE client_id = c.client_id) AS total_sales,
    (SELECT AVG(invoice_total) FROM invoices) AS average,
    (SELECT total_sales - average) AS differnece
FROM clients c
```

![select subqueries output](../images/Sandeep%20Makwana%20-%20Screen%20Shot%202022-11-26%20at%204.56.25%20PM.png)


---

**Subqueries in the FROM Clause**
> whenever we use subqueries in FROM clause we always need to spacify the alais
> it create a virtual table and we can use other operation.
```SQL
SELECT *
FROM (
    SELECT
        client_id,
        name,
        (SELECT SUM(invoice_total) FROM invoices WHERE client_id = c.client_id) AS total_sales,
        (SELECT AVG(invoice_total) FROM invoices) AS average,
        (SELECT total_sales - average) AS differnece
    FROM clients c
) AS sales_summary
```
![select subqueries output](../images/Sandeep%20Makwana%20-%20Screen%20Shot%202022-11-26%20at%204.56.25%20PM.png)

```SQL
SELECT *
FROM (
    SELECT
        client_id,
        name,
        (SELECT SUM(invoice_total) FROM invoices WHERE client_id = c.client_id) AS total_sales,
        (SELECT AVG(invoice_total) FROM invoices) AS average,
        (SELECT total_sales - average) AS differnece
    FROM clients c
) AS sales_summary
WHERE total_sales IS NOT NULL
```