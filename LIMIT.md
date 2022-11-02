**LIMIT**
```SQL
-- LIMIT

SELECT * FROM customers LIMIT 30;

SELECT * FROM customers LIMIT 6,3;  -- 6 => string 6 records skip and then next 3 records are printed

-- page 1 : 1-3
-- page 2 : 4-6
-- page 3 : 7-9.    -- we went this number so we use offset (skip)

-- LIMIT skip_value , limit_value
SELECT * FROM customers ORDER BY points DESC LIMIT 2,1;
```
