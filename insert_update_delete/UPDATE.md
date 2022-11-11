
# Update
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
