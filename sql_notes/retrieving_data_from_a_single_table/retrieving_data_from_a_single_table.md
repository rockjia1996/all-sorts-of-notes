# Retrieving Data from A Single Table


## Query Database with SELECT clause

Step 1: Choose a database
```sql
USE some_database_name;
```

Step2: Select a table in that database
```sql
SELECT col1, col2 from some_table_in_the_database;
```
```sql
SELECT * from some_table_in_the_database;
```

Step3: Do the Queries
```sql
SELECT * FROM some_table_in_the_database
WHERE  some_col > 60;
```


## SELECT clause
Basic Syntax:

To select specific columns
```sql
SELECT column_name_1, column_name_2 FROM some_table;

```
To select the specifc columns, specifying the column name after select clause. 


To select every column 
```sql
SELECT * FROM some_table;
```
To select the all the columns, * needs to be supplied after select


To mainpulate the columns
```sql
SELECT name, points + 10 FROM customers; 
``` 
The manipulation can be done by specifying the column and do logical and arithmetic operations on it

It will be better if we can assign the newly generated column after the column mainpluations. To assign an alias to a column:
```sql
SELECT name, (point + 10) * 100 AS discount_factor FROM customers
SELECT name, (point + 10) * 100 AS "discount factor" FROM customer;
```
As shown above, AS is the keyword that can be used for aliasing a column. One thing, if the new name contains space, it needs to be in the single or double quotes. If the new name does not contain space, it can be specified without quotes.


## WHERE clause
Using where clause, the queries can be filtered.
```sql
SELECT * FROM customers
WHERE points > 3000;
```

The common comparsion operators in MySQL
```sql
-- Common comparsion operators
-- >, >=, <, <=, =, <>, !=
```

To compare date
```sql
SELECT * FROM customers
WHERE birth_data > "1990-01-01"
```
Date string needs to the following format, 4 digits for years, 2 digits for month, and 2 digits for day.

To specific multiple conditions
```sql
SELECT * FROM customers
WHERE birth_date > "1990-01-01" AND points > 1000;
```
Other logical operators are NOT, OR.

To filter base on a list of constraints
```sql
SELECT * FROM customers
WHERE state IN ('VA', 'FL', 'GA');

```
### BETWEEN in WHERE
```sql
SELECT * FROM table
where points BETWEEN 1000 AND 2000;
```
BETWEEN is inclusive, in the example above, points that equals to 1000 and points that equals to 2000 will be selected.



## LIKE clause
```sql
SELECT * FROM customers
WHERE last_name LIKE "b%";
```
% means zero or more any character.
_ means one any character

## REGEXP

```sql
SELECT * FROM customer
WHERE last_name REGEXP '^field$';
```
The code above looks for the last_name that start with field and end with field.

```sql
-- ^      begin
-- $      end
-- |      or 
-- [a-f]  range
```


More examples
```sql
'field$|mac|rose'   -- end with field or exactly mac or exactly rose
'[gim]e'            -- g or i or m follows an e
'[a-h]e[x-z]'       -- one character from a to h, then e, one character from  x to z
```

## NULL
Sometimes the table may have some empty field with NULL value, to select the rows that contain a null value (in this case, phone value is null).
```sql
SELECT * FROM customer
WHERE phone IS NULL;
-- alternatively, WHERE phone IS NOT NULL;
```

## ORDER BY


