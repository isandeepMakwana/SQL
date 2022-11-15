# [INSERT statement](INSERT.md)
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

---

# [Update](UPDATE.md)
**Updating a single row**
```SQL
UPDATE invoices
SET
	payment_total =10,
    payment_date ='2019-03-01'
WHERE invoice_id =1;
```
> also we can use operations with columns

```SQL
UPDATE invoices
SET
	payment_total =invoice_total *0.5,
    payment_date =due_date
WHERE invoice_id =1;
```

**Updating a multiple row**

```SQL
UPDATE invoices
SET
	payment_total =invoice_total *0.5,
    payment_date =due_date
WHERE client_id =3; -- need to spacify a genric condition (data who have client_id =3 are updated)
```
```SQL

UPDATE invoices
SET
	payment_total =invoice_total *0.5,
    payment_date =due_date
WHERE client_id IN (3,4); -- (data who have client_id =3 or 4 are updated)
```

-- ex --
> write a sql statement to give any customers born before 1990 ,give 50 extra points
```SQL
UPDATE customers
set points = points+50
WHERE birth_date < '1990-01-01';
```

**Using subqueries in Updates**

```SQL
UPDATE invoices
SET
	payment_total = invoice_total * 0.5,
    payment_date = due_date
WHERE client_id =
			(SELECT client_id FROM clients WHERE name = 'Myworks');
```

```SQL
UPDATE invoices
SET
	payment_total = invoice_total * 0.5,
    payment_date = due_date
WHERE client_id IN
			(SELECT client_id FROM clients WHERE state IN ('CA','NY'));
```

```SQL
UPDATE orders
SET comments = 'Gold customers'
WHERE customer_id IN
	( SELECT customer_id
	FROM customers WHERE points > 3000)
```
---

# [DELETE](DELETE.md)
```SQL
use sql_invoicing;
DELETE FROM invoices;
```
```SQL

DELETE FROM invoices WHERE invoice_id =1;
```
```SQL
DELETE FROM invoices
WHERE client_id = (SELECT client_id FROM clients WHERE name = 'Myworks')
```