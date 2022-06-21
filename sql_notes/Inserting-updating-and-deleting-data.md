# Inserting Updating and Deleting Data

## Inserting a row
Basic syntax
```sql
INSERT INTO customers VALUES(...)
```
If the primary key i sset to auto increment, it is best to used DEFAULT to generate the value. 
If a column is NOT NULL (NN), you must supply a value.
Without specifying the column name like the query above, the values need to be supplied in the same order as teh order of columns.

Example on basic syntax
```sql
INSERT INTO customers
VALUES (
    DEFAULT,
    'John',
    'Smith',
    '1990-01-01',
    NULL,
    'address',
    'city',
    'CA',
    DEFAULT
);
```

Explicitly specified columns syntax
```sql
INSERT INTO customers(
    first_name,
    last_name,
    birth_date,
    address,
    city,
    state
)
VALUES (
    "John",
    "Smith",
    "1990-01-01",
    "address",
    "city",
    "CA"
)

```



