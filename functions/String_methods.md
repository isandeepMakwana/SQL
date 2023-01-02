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
