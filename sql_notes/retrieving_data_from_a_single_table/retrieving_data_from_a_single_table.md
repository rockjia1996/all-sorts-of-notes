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
Common Syntax:

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


