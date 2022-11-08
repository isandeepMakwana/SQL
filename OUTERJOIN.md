## OUTER JOIN
-   LEFT
-   RIGHT

**Convert INNER JOIN to OUTER JOIN**
```SQL
-- inner join
SELECT
c.customer_id,c.first_name , o.order_id
FROM customers c
JOIN orders o
	ON c.customer_id = o.customer_id
ORDER BY c.customer_id;


-- left outer join
SELECT c.customer_id, c.first_name , o.order_id
FROM customers c
LEFT JOIN orders o
	ON c.customer_id = o.customer_id
ORDER BY c.customer_id;

-- right outer join
SELECT c.customer_id, c.first_name , o.order_id
FROM orders o
RIGHT JOIN customers c
	ON c.customer_id = o.customer_id
ORDER BY c.customer_id
```