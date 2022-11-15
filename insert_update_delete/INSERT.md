# INSERT statement
```SQL
INSERT INTO customers
    VALUES(DEFAULT,'John','Smith','1990-01-01',NULL,'address','city','CA',DEFAULT
    );

-- OR

INSERT INTO customers
    (first_name,last_name,birth_date,address,city,state)
    VALUE ('john','Smith','1990-01-01','address','city','CA')

```

**insert multiple records in single table**
```SQL
INSERT INTO shippers (name)
VALUES ('shipper1'),
	   ('Shipper2'),
       ('Shipper3');


INSERT INTO products (name , quantity_in_stock,unit_price)
VALUES	('Product1',10,1.95),
		('Product2',11,1.95),
        ('Product3',12,1.95);
```

---


**Creating a copy of a Table**

> if you copy one table to another table it copy's only data not create a primary and not null or forign key

```SQL
CREATE TABLE orders_archived
AS
SELECT * FROM orders;
```

>insert all data of one table to other table but need same structure or provie a same structure
```SQL
INSERT INTO orders_archived
SELECT * FROM orders
WHERE order_date < '2019-01-01'
```
```SQL
-- ex --
USE sql_invoicing;

CREATE TABLE invoice_archived
AS
SELECT
	i.invoice_id,
    i.number,
    c.name as client,
    i.invoice_total,
    i.payment_total,
    i.invoice_date,
    i.payment_date,
    i.due_date
FROM invoices i
JOIN clients c
	USING(client_id)
WHERE payment_date IS NOT NULL;
```
