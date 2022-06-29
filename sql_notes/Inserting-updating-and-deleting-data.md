# Inserting Updating and Deleting Data

## Inserting a row
Basic syntax
```sql
INSERT INTO customers VALUES(...)
```
If the primary key is set to auto increment, it is best to used DEFAULT to generate the value. 
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

## Creating a Copy of a Table
To create a table in database
```sql
CREATE TABLE table_name AS
-- HERE GOES YOUR RECORDS 
```

Example
```sql
CREATE TABLE invoice_archived as SELECT i.invoice_id,
    i.number,
    c.name,
    i.invoice_total,
    i.payment_total,
    i.invoice_date,
    i.due_date,
    i.payment_date FROM
    invoice i
        JOIN 
    client c on i.client_id = c.client_id
WHERE i.payment_date IS NOT NULL;
```
Note that the WHERE clause goes after JOIN clause.

## Updating a Single Row
```sql
UPDATE invoices
SET payment_total = 10, payment_date = '2019-01-01'
WHERE invoice_id = 1;
```
We specify the invoice table after UPDATE, then using SET to specify the columns and values that we want to update, finally using WHERE to apply the update conditionally.

To update based on columns without hard code values
```sql
UPDATE invoices
SET payment_total = invoice_total * 2,
    payment_date = due_date;
```

## Updating Multiple Rows
By default, MySQL workbench runs in a safe mode that aonly allows you to update single row at a time. To bypass that you need to change the setting as following:
    Edit -> Preference -> SQL Editor -> Uncheck safe update
```sql
UPDATE invoices
SET payment_total = invoice_total * 0.5,
    payment_date = due_date
WHERE client_id IN (3, 4)
```
Note that the WHERE clause is optional.

## Using Subqueries In Update
```sql
UPDATE invoices
SET 
    payment_total = invoice_total * 0.5,
    payment_date = due_date
WHERE client_id = (SELECT client_id FROM clients WHERE name = "Myworks");
```

## Deleting Rows
To delete all the records in a table
```sql
DELETE FROM invoice;
```

To delete with the given condition
```sql
DELETE FROM invoice
WHERE client_id = (SELECT client_id FROM clients WHERE name = "Myworks");
```
