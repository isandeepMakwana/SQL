
**INNER JOIN**
> INNER JOIN and  JOIN is same

```SQL
SELECT *
FROM orders
JOIN customers
	ON orders.customer_id = customers.customer_id;
```

```SQL
SELECT order_id , orders.customer_id, first_name , last_name
FROM orders
JOIN customers
	ON orders.customer_id = customers.customer_id;
```

**create alias **
```SQL
SELECT order_id , o.customer_id, first_name , last_name
FROM orders o
INNER JOIN customers c
	ON o.customer_id = c.customer_id;
```

**JOIN with other database table**

```SQL
-- we need to provide database name with table

SELECT * FROM order_items oi
JOIN sql_inventory.products p   -- we need to provide database name with table
	ON oi.product_id = p.product_id;


```

**self join**

```SQL
use sql_hr;

SELECT e.employee_id ,e.first_name, e.salary , m.first_name AS manager
FROM employees e
JOIN employees m
ON e.reports_to = m.employee_id;
```

**join in multiple table**

```SQL
-- select * FROM orders;
-- select * from customers;
-- select * from order_statuses;

SELECT  o.order_id ,o.order_date,c.first_name , c.last_name, os.name AS status
FROM orders o
JOIN customers c
	ON o.customer_id = c.customer_id
JOIN order_statuses os
	ON o.status=os.order_status_id

```
