[**IS NULL**](ISNULL.md)

```SQL

-- IS NULL
SELECT * FROM customers WHERE phone IS NULL; -- phone no. is null

-- IS NOT NULL
SELECT * FROM customers WHERE phone IS NOT NULL; -- phone no. is not null

SELECT * FROM orders WHERE shipped_date IS NULL;

```