
# DELETE
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