**LIKE**

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