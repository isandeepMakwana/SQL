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


**outer join with multitable**
```SQL
SELECT c.customer_id,c.first_name,sh.name AS shipper FROM customers c
LEFT JOIN orders o
	ON c.customer_id = o.customer_id
LEFT JOIN shippers sh
	ON o.shipper_id = sh.shipper_id
ORDER BY c.customer_id;
```
```SQL
-- ex--
SELECT o.order_date,o.order_id , c.first_name ,sh.name AS shipper ,os.name as status
FROM orders o
JOIN customers c
	ON c.customer_id = o.customer_id
LEFT JOIN shippers sh
	ON o.shipper_id = sh.shipper_id
JOIN order_statuses os
	ON os.order_status_id =o.status
```
