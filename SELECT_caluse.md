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
