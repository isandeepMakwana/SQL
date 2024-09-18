
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