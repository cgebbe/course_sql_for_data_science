# Week 2

### Basics of Filtering

Filtering also helps query performance on server and client side!

```sqlite
SELECT column1, columns2
FROM table_name
WHERE column_name <operator> <left_side>
/*
operator
= equal -- WHERE FirstName = 'Alice';
<> not equal
<, >, <=, >= smaller, larer
BETWEEN -- WHERE UnitsInStock BETWEEN 15 AND 80;
IS NULL -- WHERE ProductName IS NULL;
*/
```

### Advanced Filtering

```sqlite
WHERE SupplierId IN (9,10,11);
WHERE ProductName = 'Tofu' OR 'Konbu'; -- similar to || in C++, not | !
```

IN is better than OR in the sense of....

- executes faster
- don't have to think about order
- can contain another SELECT for subqueries

```sqlite
WHERE SupplierID=9 OR SupplierID=11 AND UnitPrice>15; -- returns some prices less than 15
WHERE SupplierID=9 OR (SupplierID=11 AND UnitPrice>15); -- this is probably what SQL executes

WHERE (SupplierID=9 OR SupplierID=11) AND UnitPrice>15; -- correct
-- --> Better use parenthesis always when mixing AND and OR
```

NOT operator

```sqlite
WHERE NOT City='London' AND NOT City='Seattle'
```

### Using wildcards

Wildcards `%`...

- can only be used with strings
- will NOT match `NULL`

```sqlite
-- % wildcard
'%PIZZA' -- get strings ending with Pizza
'PIZZA%'
'%PIZZA%'
'S%E'
where email LIKE 't%@gmail.com'

-- _ wildcard
'_pizza' -- matches only a single character, but not supported by all DBMS
WHERE size LIKE '_pizza'

-- [ and ] wildcard
-- matches a set of characters, but not supported by SQLite

```

Downsides of wildcards

- uses longer to run than e. g. `>`

### Sorting with ORDER BY

```sqlite
SELECT something
FROM database
ORDER BY characteristic -- not retrieved, but still possible to sort by!
-- ORDER BY 2,3 -- means 2nd and 3rd column, however not advised
-- ORDER BY characteristic DESC, another ASC -- ASC is default
```

- can use multiple columns (order relevant!)

### Math operators

```sqlite
-- Available operators are +, -, *, /
SELECT ProductID, UnitsOnOrder, UnitPrice
, UnitsOnOrder * UnitPrice AS Total_Order_Cost
FROM PRODUCTS
-- , (UnitPrice - Discount) / Quantity AS Total_Cost
```

operation order as in typical math

- () - paranthesis
- ^ - exponents
- *
- /
- +
- -

### Aggregate functions

```sqlite
-- AVG, COUNT, MIN, MAX, SUM
SELECT AVG(UnitPrice) AS avg_price FROM Products
SELECT COUNT(*) AS total_customers FROM Customers -- includes NULL
SELECT COUNT(CustomerID) AS total_customers FROM Customers -- excludes NULL
SELECT MAX(UnitPrice) AS max_price, MIN(UnitPrice) AS min_price
SELECT SUM(UnitPrice * UnitsInStock) AS total_price

-- DISTINCT to ignore duplicates, similar to np.unique() 
-- if not specified, ALL is assumed
-- cannot use DISTINCT on COUNT(*)
SELECT COUNT(DISTINCT CustomerID) FROM Customers
```

### Grouping data

Using the aggregate functions from above....

```sqlite
SELECT Region, COUNT(CustomerID) AS total_customers
FROM Customers
GROUP BY Region -- without this line, error, since not clear how to count
-- Every column in SELECT must be present in GROUP BY except aggregated calculations
-- NULLs will be grouped together if columns contain NULL

SELECT CustomerID, Count(*) AS orders
FROM Orders
WHERE UnitPrice>=4
GROUP BY CustomerID HAVING COUNT(*) >= 2;
/*
WHERE works before grouping (on rows)
HAVING works after grouping (on groups)
*/ 
```



### Putting it all together

```sqlite
-- Order of statements
SELECT
FROM
WHERE
GROUP BY
HAVING
ORDER BY
(LIMIT)
```

### Practice quiz

salary_range_by_job_classification contains the following columns:

- SetID
- Job_Code 
- Eff_Date 
- Sal_End_Date 
- Salary_setID 
- Sal_Plan 
- Grade 
- Step 
- Biweekly_High_Rate 
- Biweekly_Low_Rate 
- Union_Code 
- Extended_Step 
- Pay_Type



## Readings

### SQL for python

https://pypi.org/project/python-sql/ is a library to write SQL queries with python

```python
>>> from sql import *
>>> from sql.aggregate import *
>>> from sql.conditionals import *

>>> user = Table('user')
>>> select = user.select()
>>> tuple(select)
('SELECT * FROM "user" AS "a"', ())
```

## Module 2 Coding Assignment

![img](week2.assets/ChinookDatabaseSchema.png)