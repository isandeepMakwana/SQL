**Numeric functions**
<br>
[Reference](https://www.w3schools.com/mysql/mysql_ref_functions.asp)

```SQL
SELECT ROUND(5.73)
```
---


> ROUND
- ROUND(5.73) => 6
- ROUND(5.7345 , 1) => 5.7
- ROUND(5.7345, 2) => 5.73

> TRUNCATE

- TRUNCATE(5.7345, 2) => kept 5.73 (2 digits) and removing other digits

> CEILING

- CEILING(5.2) ==> it return smallest Integer that is equal_to (=) or grater_then (>) this number [output=6] and it's diffrent from round function.{=>}

> FLOOR

- FLOOR(5.2) ==> it return smallest Integer that is equal_to (=) or less_then (<) this number [output=5] and it's diffrent from round function.{=<}

> ABS
- ABS(-5.2) => 5.2

> RAND
- RAND() => genreating a random number between 0 to 1 (like 0.00596860889901...)
