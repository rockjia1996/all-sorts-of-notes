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

## Insert to Multiple Tables
Basic Syntax
```sql
INSERT INTO shippers(name)
VALUES 
    ('shipper1'),
    ('shipper2'),
    ('shipper3')

```
We can use comma to sepreate different values (rows) that we want to insert.

## Inserting Hierarchical Rows (Insert Rows to Multiple Tables)
```sql
INSERT INTO orders (customer_id, order_date, status)
VALUES (1, "2019-01-01", 1);

INSERT INTO order_items
VALUES 
    (LAST_INSERT_ID(), 1, 1, 2.95),
    (LAST_INSERT_ID(), 2, 2, 3.95);
```
orders table contians order_id but not the details of the items.
order_items table contains order_id and the details of the items.
One order in orders table may have one or more entries (children) in order_items table. They have a parent-child relationship.
LAST_INSERT_ID() give the primary key of the last inserted record.


