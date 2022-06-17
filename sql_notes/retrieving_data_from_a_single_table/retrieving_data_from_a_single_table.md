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