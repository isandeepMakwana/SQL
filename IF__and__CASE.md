
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

