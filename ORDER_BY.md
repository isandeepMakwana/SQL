**Order by**
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