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
-- it find.   ge
-- 			 ie
-- 			 me


SELECT * FROM customers WHERE last_name REGEXP 'e[fmq]';
-- it find.   ef
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
## [schemas](SCHEMAS.md)

<div style="width:400px ; height:200px">

![customers](images/Sandeep%20Makwana%20-%20Screen%20Shot%202022-11-02%20at%209.09.05%20AM.png)
![orders](images/Sandeep%20Makwana%20-%20Screen%20Shot%202022-11-02%20at%209.09.28%20AM.png)
![order_statuses](images/Sandeep%20Makwana%20-%20Screen%20Shot%202022-11-02%20at%209.10.30%20AM.png)
![employees](images/Sandeep%20Makwana%20-%20Screen%20Shot%202022-11-02%20at%209.13.10%20AM.png)
![order_items](images/Sandeep%20Makwana%20-%20Screen%20Shot%202022-11-02%20at%209.14.18%20AM.png)
![other_database_prducts table](images/Sandeep%20Makwana%20-%20Screen%20Shot%202022-11-02%20at%209.14.43%20AM.png)
![products](images/Sandeep%20Makwana%20-%20Screen%20Shot%202022-11-02%20at%209.16.31%20AM.png)

<div>
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

---

[**subqueries**](subqueries/subqueries.md)

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

![select subqueries output](images/Sandeep%20Makwana%20-%20Screen%20Shot%202022-11-26%20at%204.56.25%20PM.png)


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

![select subqueries output](images/Sandeep%20Makwana%20-%20Screen%20Shot%202022-11-26%20at%204.56.25%20PM.png)


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

---

# SQL FUNCTIONS

**Numeric functions**
<br>
[Reference](https://www.w3schools.com/mysql/mysql_ref_functions.asp)

```SQL
SELECT ROUND(5.73)
```
---


> ROUND
- ROUND(5.73) => 6
- ROUND(5.7345 , 1) => 5.7
- ROUND(5.7345, 2) => 5.73

> TRUNCATE

- TRUNCATE(5.7345, 2) => kept 5.73 (2 digits) and removing other digits

> CEILING

- CEILING(5.2) ==> it return smallest Integer that is equal_to (=) or grater_then (>) this number [output=6] and it's diffrent from round function.{=>}

> FLOOR

- FLOOR(5.2) ==> it return smallest Integer that is equal_to (=) or less_then (<) this number [output=5] and it's diffrent from round function.{=<}

> ABS
- ABS(-5.2) => 5.2

> RAND
- RAND() => genreating a random number between 0 to 1 (like 0.00596860889901...)

---

**String methods**
> SQL follows 1 based indexing

- LENGTH('sky')
- UPPER('sky')
- LOWER('Sky')
- LTRIM('     Sky')
- RTRIM('Sky        ')
- TRIM('  Sky  ')
- LIFT('Kindergarten' , 4) => Kind
- RIGHT('Kindergarten',  6) => garten
- SUBSTRING('Kindergarten' , 3 , 5)=>startposition, lengthofword] ==> nderg
- SUBSTRING('Kindergarten' , 3) ==> dergarten
- LOCATE('n','Kindergarten') => 3 (position of n)
- LOCATE('q','Kindergarten') => 0 (it return 0 becouse q is not present in this string)
- LOCATE('garten','Kindergarten') => 7
- REPLACE('Kindergarten','garten','garden') => Kindergarden
- CONCAR('first','last') => firstlast

--ex--
```SQL
SELECT CONCAT(first_name , ' ',last_name) AS full_name
FROM customers
```
---

**DATE Functions**

- NOW()
- CURDATE()
- CURTIME()
- YEAR(NOW()) => 2022
- MONTH(NOW()) => 11
- DAY(NOW()) => 19
- HOUR(NOW() => 4
- MINITE(NOW()) =>40
- SECOND(NOW()) => 20

- DAYNAME(NOW()) => Monday
- MONTHNAME(NOW()) => March

- EXTRACT(YEAR FROM NOW()) => 2022

-- ex --

```SQL
SELECT *
FROM orders
WHERE YEAR(order_date) = YEAR(NOW())
```
**Date Formating**

- DATE_FORMAT(NOW(),'%y') => 22
- DATE_FORMAT(NOW(),'%Y') => 2022
- DATE_FORMAT(NOW(),'%m %Y') => 03 2022
- DATE_FORMAT(NOW(),'%M %Y') => March 2022
- DATE_FORMAT(NOW(),'%M %d %Y') => March 11 2022

- TIME_FORMAR(NOW(), '%H:%i %p') => 12:58 PM
- TIME_FORMAR(NOW(), '%H:%i %a') => 12:58 AM



**Calculation in date**
- DATE_ADD(NOW(), INTERVAL 1 DAY) => simply add 1 day (2022-03-12 13:26:26)
- DATE_ADD(NOW(), INTERVAL 1 YEAR) => simply add 1 year (2023-03-12 13:26:26)

- DATE_ADD(NOW(), INTERVAL -1 YEAR) => simply SUB 1 year (2021-03-12 13:26:26)
- DATE_SUB(NOW(), INTERVAL 1 YEAR) => simply SUB 1 year (2021-03-12 13:26:26)

- DATEDIFF('2019-01-05','2019-01-01') => 4 (it only returns differnce of date not time)
- DATEDIFF('2019-01-01','2019-01-05') => - 4 (it only returns differnce of date not time)

- TIME_TO_SEC('09:00') - TIME_TO_SEC('09:02') => -120 sec
- TIME_TO_SEC('09:02') - TIME_TO_SEC('09:00')  => 120


---

<mark>IFNULL vs COALESCE<mark>

**IFNULL**

```SQL

USE sql_store;
SELECT
    order_id,
    IFNULL(shipper_id, 'Not assigned') AS shipper
FROM orders


-- output : replaced behalf of the null with Not assigned
```

**COALESCE**
```SQL
SELECT
    order_id,
    COALESCE(shipper_id , comments, 'Not assigned') AS shipper
FROM orders
-- if shipper_id is null replaced with comments values , but if comments values is also null then it replaced with 'Not Assigned'

-- shipper_id is null then return commments value but the comments value is also null then return 'not assigned'

```


--ex--
```SQL
SELECT
    CONCAT(first_name , ' ', last_name) AS customer,
    COALESCE(phone ,'Unknown') AS phone
FROM customers

-- or --

SELECT
    CONCAT(first_name , ' ', last_name) AS customer,
    IFNULL(phone ,'Unknown') AS phone
FROM customers

```


---

<mark> IF statement vs CASE operator<mark>

 **IF statement**

 `IF(expression , first , second)`

```SQL
SELECT
    order_id,
    order_date,
    IF(
        YEAR(order_date) = YEAR(NOW()),
        'Active',
        'Archived'
    ) AS category
FROM orders
```


```SQL
SELECT
    prodcut_id,
    name,
    COUNT(*) AS orders
    IF(COUNT(*) > 1 , 'Many times', 'Once') AS frequency
FROM products
JOIN order_items USING (product_id)
GROUP BY product_id , name

-- or --

SELECT
	product_id,
    name,
    (SELECT COUNT(*) FROM order_items WHERE product_id = p.product_id) AS orders,
    (SELECT IF(orders=1,'once','Manytimes'))
FROM products p
HAVING orders>0;
```

**CASE operator**
> if you want multiple conditions

```SQL
SELECT
    order_id,
    CASE
        WHEN YEAR(order_date) = YEAR(NOW()) THEN 'Active'
        WHEN YEAR(order_date) = YEAR(NOW())-1 THEN 'Last Year'
        WHEN YEAR(order_date) = YEAR(NOW())-1 THEN 'Archived'
        ELSE 'Future'
    END AS category
FROM orders

```
```SQL
SELECT
	CONCAT(first_name,' ',last_name) AS customer,
    points,
    CASE
		WHEN (points >=3000) THEN 'GOLD'
        WHEN points >=2000 THEN 'SELVER'
        ELSE 'BRONZE'
	END AS MADDLE
FROM customers
ORDER BY points DESC;
```

