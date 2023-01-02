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
