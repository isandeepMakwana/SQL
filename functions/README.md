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
