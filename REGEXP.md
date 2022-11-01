**REGEXP**
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
SELECT * FROM customers WHERE last_name REGEXP 'B[RU]';

```
