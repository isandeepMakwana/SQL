# Learn SQL

[**SELECT caluse**](SELECT_caluse.md)

```SQL
    SELECT
	last_name ,
    first_name,
    points ,
    (points +10) * 100 AS discount_factor  --you can use arthmatic opreation !
    FROM customers;
```
```SQL
    SELECT
	DISTINCT state --return Uniqic value !🤩
    FROM customers;
```
---
[**Where clause**](WHERE_CLAUSE.md)

```SQL
-- operation with date
SELECT * FROM customers WHERE birth_date > ' 1990-01-01 ';

SELECT count(*) FROM orders WHERE order_date >= ' 2019-01-01 ';
```

---

[**AND , OR , NOT**](AND_OR_NOT.md)
```SQL
-- AND execute 1st (*)
-- OR execute 2nd (+)
/* always use ( ) */

SELECT * FROM customers WHERE birth_date > '1990-01-01' OR ( points > 1000 AND state= 'VA')
```

```SQL
SELECT * FROM order_items WHERE order_id=6 AND unit_price * quantity > 30 -- you can use arthmatic operation after Where clause;
```

---


[**IN**](IN.md)

```SQL
SELECT * FROM customers WHERE state IN ('VA','FL','GA');
```
---

[**BETWEEN**](BETWEEN.md)
```SQL
SELECT * FROM customers WHERE points BETWEEN 1000 AND 3000;
-- SELECT * FROM customers WHERE points >=1000 AND points<=3000;
SELECT * FROM customers WHERE birth_date BETWEEN '1990-01-01' AND '2000-01-01';
```

---

[**LIKE**](LIKE.md)(old_method)

```SQL

-- '%' any number of characters

SELECT * FROM customers WHERE last_name LIKE 'b%'; -- it find all records where last_name contains b at biginning.
SELECT * FROM customers WHERE last_name LIKE 'brush%';

SELECT * FROM customers WHERE last_name LIKE '%b%'; -- it find all records where last_name contains b in ('starting ' , 'middle' ,'ending') please focuse on this.
SELECT * FROM customers WHERE last_name LIKE '%y';

-- '_' single character
SELECT * FROM customers WHERE last_name LIKE '_y'; -- it pring all records where last name have length of 2 and the last chacter is y.
SELECT * FROM customers WHERE last_name LIKE '_____t'; -- -- it pring all records where last name have length of 5 and the last chacter is t.
SELECT * FROM customers WHERE last_name LIKE 'b____y';
--  -- it pring all records where last name have length of 5 and the first chacter is b and last is y.



/* print all records where address contains trail or avenue */
SELECT * FROM customers WHERE address LIKE '%TRAIL%' OR address LIKE '%AVENUE%';
/* print all records where phone number last charcter in not 9 */
SELECT * FROM customers WHERE phone_number NOT LIKE '%9';

```
---
[**REGEXP**](REGEXP.md) (new_method)

```SQL

-- ^ bignning
-- $ end
-- | logical or
-- [fmq] cantines
-- [a-h] range a to h

SELECT * FROM customers WHERE last_name REGEXP 'field'; -- is equal to %field%

SELECT * FROM customers WHERE last_name REGEXP '^b'; -- is equal to %b

SELECT * FROM customers WHERE last_name REGEXP 'y$'; -- is equal to y%
SELECT * FROM customers WHERE last_name REGEXP 'field'; -- is equal to %field%
SELECT * FROM customers WHERE last_name REGEXP 'field|mac';  -- is equal to %field% or %mac%
SELECT * FROM customers WHERE last_name REGEXP 'field|mac|rose'; -- is equal to %field% or %mac% or %rose%
SELECT * FROM customers WHERE last_name REGEXP 'field$|mac$'; -- is equal to field% or mac%

SELECT * FROM customers WHERE last_name REGEXP 'field$|^mac|rose'; -- is equal to field% or %mac or %rose%

SELECT * FROM customers WHERE last_name REGEXP '[gie]e';
-- it find.   		 ge
-- 			 ie
-- 			 me


SELECT * FROM customers WHERE last_name REGEXP 'e[fmq]';
-- it find.   		 ef
-- 			 em
-- 			 eq

SELECT * FROM customers WHERE last_name REGEXP '[a-h]e';

--EX:-
-- get the customers whose
-- 		first name are ELKA or AMBUR
-- 		last name end with EY or ON
--      last name start with MY or contains SE
--      last name contains B followed by R or U
SELECT * FROM customers WHERE first_name REGEXP 'ELKA|AMBUR';
SELECT * FROM customers WHERE last_name REGEXP 'EY$|ON$';
SELECT * FROM customers WHERE last_name REGEXP '^MY|SE';
SELECT * FROM customers WHERE last_name REGEXP 'B[RUP]';

```

---
[**IS NULL**](ISNULL.md)

```SQL

-- IS NULL
SELECT * FROM customers WHERE phone IS NULL; -- phone no. is null

-- IS NOT NULL
SELECT * FROM customers WHERE phone IS NOT NULL; -- phone no. is not null

SELECT * FROM orders WHERE shipped_date IS NULL;

```
---

[**Order by**](ORDER_BY.md)
```SQL
SELECT * FROM customers
-- WHERE customer_id =1
ORDER BY first_name;
```



```SQL

SELECT * FROM customers ORDER BY first_name DESC;
SELECT * FROM customers ORDER BY state,first_name;
SELECT * FROM customers ORDER BY state DESC,first_name DESC;

-- you can sort data with Alias

SELECT first_name , last_name , 10 AS points FROM customer
ORDER BY points , first_name;
SELECT first_name , last_name , 10*point_value/total_number AS points FROM customer
ORDER BY points , first_name;

-- EX:

SELECT * FROM order_items WHERE order_id=2 ORDER BY quantity*unit_price DESC;  -- you can use arthmatic operation !

-- OR

SELECT *, quantity*unit_price AS total_price FROM order_items WHERE order_id=2 ORDER BY total_price DESC;

```

```SQL
-- using column number (NOT Recommended)
SELECT first_name , last_name , 10 AS points FROM customer
ORDER BY 1,2; -- 1 means first_name and 2 means last_name
```
---
[**LIMIT**](LIMIT.md)
```SQL
-- LIMIT

SELECT * FROM customers LIMIT 30;

SELECT * FROM customers LIMIT 6,3;  -- 6 => string 6 records skip and then next 3 records are printed

-- page 1 : 1-3
-- page 2 : 4-6
-- page 3 : 7-9.    -- we went this number so we use offset (skip)

-- LIMIT skip_value , limit_value
```
![output](images/Sandeep%20Makwana%20-%20Screen%20Shot%202022-11-01%20at%204.14.11%20PM.png)
```SQL
-- EX :
SELECT * FROM customers ORDER BY points DESC LIMIT 3;
```
---

# "Retrieving-data-from-multiple-table"

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
**use composit key to join**

```SQL
SELECT *
FROM order_items oi
JOIN order_item_notes oin
	ON oi.order_id = oin.order_id
	AND oi.product_id = oin.product_id;
```
## schemas [link](SCHEMAS.md)

![customers](images/Sandeep%20Makwana%20-%20Screen%20Shot%202022-11-02%20at%209.09.05%20AM.png)
![orders](images/Sandeep%20Makwana%20-%20Screen%20Shot%202022-11-02%20at%209.09.28%20AM.png)
![order_statuses](images/Sandeep%20Makwana%20-%20Screen%20Shot%202022-11-02%20at%209.10.30%20AM.png)
![employees](images/Sandeep%20Makwana%20-%20Screen%20Shot%202022-11-02%20at%209.13.10%20AM.png)
![order_items](images/Sandeep%20Makwana%20-%20Screen%20Shot%202022-11-02%20at%209.14.18%20AM.png)
![other_database_prducts table](images/Sandeep%20Makwana%20-%20Screen%20Shot%202022-11-02%20at%209.14.43%20AM.png)
![products](images/Sandeep%20Makwana%20-%20Screen%20Shot%202022-11-02%20at%209.16.31%20AM.png)

---
---
# OUTER JOIN
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

Note : Recommanded to always use same join in multiple table  like LEFT , LEFT


**self outer join**

```SQL
SELECT
	e.employee_id,
	e.first_name,
	m.first_name AS manager
FROM employees e
LEFT JOIN employees m
	ON e.reports_to = m.employee_id
```

---
[**USING**](USING.md)

instead of 'ON' we use USING
it simplify our Query  but we only use 'USING' clause when the column name is same in both tables


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
---
[**NATURAL JOIN**](NATURAL%20JOIN.md)

In 'Natural Join' we don't need to specify the condition
it automatically locates the simller column and join bases of them.
```SQL
SELECT
    o.order_id,
    c.first_name,
FROM orders o
NATURAL JOIN customers c
```
NOTE :<b> not recommanded</b>

---
[**CROSS JOIN**](CROSS%20JOIN.md)

The CROSS JOIN keyword returns all matching records from both tables whether the other table matches or not.
table1 records
id,name
1,a
2,b

table 2 records
id,class
1,x
2,xII

output:

a,x
a,xII
b,x
b,XII

```SQL
SELECT name , class
FROM table1
CROSS JOIN table2
ORDER BY name
```
```SQL
SELECT
    c.frist_name AS customer,
    p.name AS product
FROM customers c
CROSS JOIN products p
ORDER BY c.frist_name
```
**implecit syntax**
```SQL
SELECT
    c.frist_name AS customer,
    p.name AS product
FROM customers c , products p
ORDER BY c.first_name
```

NOTE:
If you add a WHERE clause (if table1 and table2 has a relationship), the CROSS JOIN will produce the same result as the INNER JOIN clause

---

[**UNION**](UNION.md)

it used for combine 2 and more Queries

```SQL
SELECT
    order_id,
    order_date,
    'Active' AS status
FROM orders
WHERE order_date >= '2019-01-01'

UNION

SELECT
    order_id,
    order_date,
    'Archived' AS status
FROM orders
WHERE order_date < '2019-01-01';
```

```SQL
SELECT first_name,
FROM archived_orders
UNION
SELECT name
FROM orders
```

--ex--
```SQL
SELECT c.customer_id , c.first_name , c.points, 'GOLD' AS type
FROM customers c WHERE c.points > 3000
UNION
SELECT c.customer_id , c.first_name , c.points, 'Silver'
FROM customers c WHERE c.points BETWEEN 2000 AND 3000
UNION
SELECT c.customer_id , c.first_name , c.points, 'Bronze'
FROM customers c WHERE c.points < 2000
ORDER BY first_name
```


---


# [**aggregate Functions**](Aggregate_Functions.md)

- MAX()
- MIN()
- AVG()
- SUM()
- COUNT()


```SQL
SELECT
    MAX(invoice_total) AS highest,
    MIN(invoice_total) AS lowest,
    AVG(invoice_total) AS average
FROM invoices
```
```SQL
SELECT
    MAX(payment_date) AS highest,
    MIN(invoice_total) AS lowest,
    AVG(invoice_total) AS average
FROM invoices
```

```SQL
SELECT
    MAX(invoice_total) AS highest,
    MIN(invoice_total) AS lowest,
    AVG(invoice_total) AS average,
    SUM(invoice_total) AS total,
    COUNT(invoice_total) AS number_of_invoices
    COUNT(payment_date) AS count_of_payments
FROM invoices
```

```SQL
SELECT
    MAX(invoice_total) AS highest,
    MIN(invoice_total) AS lowest,
    AVG(invoice_total) AS average,
    SUM(invoice_total * 1.1) AS total,
    COUNT(*) AS total_records
FROM invoices
WHERE invoice_date  >'2019-07-01'
```



```SQL
SELECT
    MAX(invoice_total) AS highest,
    MIN(invoice_total) AS lowest,
    AVG(invoice_total) AS average,
    SUM(invoice_total * 1.1) AS total,
    COUNT(DISTINCT client_id) AS total_records
FROM invoices
WHERE invoice_date  >'2019-07-01'
```

-- ex --

```SQL
SELECT
    'First half of 2019' AS date_range,
    SUM(invoice_total) AS total_sales,
    SUM(payment_total) AS total_payments,
    SUM(invoice_total - payment_total) AS What_we_expected
FROM invoices
WHERE invoice_date
     BETWEEN '2019-01-01' AND '2019-06-30'

UNION

SELECT
    'Second half of 2019' AS date_range,
    SUM(invoice_total) AS
    SUM(payment_total) AS total_payments,
    SUM(invoice_total - payment_total) AS What_we_expected
FROM invoices
WHERE invoice_date
    BETWEEN '2019-07-01' AND '2019-12-31'

UNION

SELECT
    'Total' AS date_range,
    SUM(invoice_total) AS
    SUM(payment_total) AS total_payments,
    SUM(invoice_total - payment_total) AS What_we_expected
FROM invoices
WHERE invoice_date
    BETWEEN '2019-01-01' AND '2019-12-31'
```
---

# [**GROUP BY**](GROUP_BY.md)

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
---

[**HAVING**](HAVING.md)

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
---

# [**ROLLUP**](ROLLUP.md)
> it basiclly calculate the sum of values.

```SQL
SELECT
    client_id,
    SUM(invoice_total) AS total_sales
FROM invoices
GROUP BY client_id WITH ROLLUP
```

```SQL
SELECT
    client_id,
    SUM(invoice_total) AS total_sales
FROM invoices
GROUP BY client_id WITH ROLLUP
```

```SQL
SELECT
    state,
    city,
    SUM(invoice_total) AS total_sales
FROM invoices i
JOIN clients c USING (client_id)
GROUP BY state, city WITH ROLLUP
```


```SQL

SELECT
    payment_method,
    SUM(amount) AS total
FROM payments
GROUP BY payment_method WITH ROLLUP

```


```SQL
SELECT
    pm.name AS payment_method,
    SUM(amount) AS total
FROM payments p
JOIN payment_methods pm
    ON p.payment_method = pm.payment_method_id
GROUP BY pm.name WITH ROLLUP
```
