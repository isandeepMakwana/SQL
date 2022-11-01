# SQL CheetShet

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