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
