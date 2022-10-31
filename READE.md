# SQL CheetShet

## SELECT caluse


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
	DISTINCT state --return Uniqic value !
    FROM customers;
```

**Where clause**

```SQL
-- operation with date
SELECT * FROM customers WHERE birth_date > ' 1990-01-01 ';

SELECT count(*) FROM orders WHERE order_date >= ' 2019-01-01 ';
```
 **Order by**
```SQL
SELECT * FROM customers
-- WHERE customer_id =1
ORDER BY first_name;
```

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
**IN**

```SQL
SELECT * FROM customers WHERE state IN ('VA','FL','GA');
```

**BETWEEN**
```SQL
SELECT * FROM customers WHERE points BETWEEN 1000 AND 3000;
-- SELECT * FROM customers WHERE points >=1000 AND points<=3000;
SELECT * FROM customers WHERE birth_date BETWEEN '1990-01-01' AND '2000-01-01';
```


```SQL

-- LIKE
-- '%' any number of characters

SELECT * FROM customers WHERE last_name LIKE 'b%'; -- it find all last_name those contains b at biginning.
SELECT * FROM customers WHERE last_name LIKE 'brush%';

SELECT * FROM customers WHERE last_name LIKE '%b%'; -- it find all last_name that contains b in ('starting ' , 'middle' ,'ending') please focuse on this.
SELECT * FROM customers WHERE last_name LIKE '%y';

-- '_' single character
SELECT * FROM customers WHERE last_name LIKE '_y'; -- it pring all the last name that have length of 2 and the last chacter is y.
SELECT * FROM customers WHERE last_name LIKE '_____t'; -- -- it pring all the last name that have length of 5 and the last chacter is t.
SELECT * FROM customers WHERE last_name LIKE 'b____y';
--  -- it pring all the last name that have length of 5 and the first chacter is b and last is y.


SELECT * FROM customers WHERE address LIKE '%TRAIL%' OR address LIKE '%AVENUE%';
SELECT * FROM customers WHERE phone_number  NOT LIKE '%9'





```