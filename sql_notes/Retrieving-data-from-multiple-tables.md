# Retrieving data from multiple tables


## Select Columns From Multiple Tables, Using INNER JOIN / JOIN
```sql
SELECT * from orders
INNER JOIN customers
    ON orders.customer_id = customers.customer_id;
```
The code above select data from orders and customers tables. The selection is based on the ON clause. In the ON clause, the condition is set to compare if the customer_id column in both tables. If the customer_id value in one of records in orders table matches the customer_id value in one of records in customer_id, then the selected columns of two records will be join. That is the record in customers table appends to the record on the orders table.

The operation above is called inner join. We also can simplfy the query by not explicit state INNER, by default JOIN is inner join.
```sql
SELECT * FROM orders
JOIN customers
    ON orders.customer_id = customers.customer_id;
```

## Compoound Join Conditions
Sometimes that values in a single column can be duplicated which cause us to be unable to uniquely identify a row solely based on a single column. We may need to combine one or more columns to uniquely identifying a row.
```sql
SELECT 
    *
FROM 
    order_items oi
    JOIN 
    order_item_notes oin 
        ON oi.order_id = oin.order_id AND oi.product_id = oin.product_id;
```

## Outer Join
INNER JOIN joins based on whether the conditions are matched in two records. 
Outer join joins based on specifying the table that is included regardless the conditions and conditions.
There are two types of outer joins, LEFT JOIN and RIGHT JOIN. 
```sql
SELECT
    *
FROM
    table_1         -- left table
LEFT JOIN 
    table_2         -- right table
    ON some_condition
```
The query about will return all the records in table_1 regardless it matches the condition or not. For the unmatched columns, the value of field of the column will be null. For the matched result, it appends matched record in table_2 to the record in the table_1.

LEFT JOIN: Include all the records in the left table regardless the conditions.
RIGHT JOIN: Include all the records in the right tbale regarless the conditions.

Note: You should avoid alternative the LEFT JOIN and RIGHT JOIN like crazy. Stick to one type (usually LEFT JOIN) JOIN so that you can have an easiler time to picture what's going on. 

## Outer Join Between Multiple Tables
The following is an example that using outer join multiple tables. Note that outer join can be done by using the same table multiple time as well.
```sql
SELECT c.customer_id, c.first_name, o.order_id, sh.name AS shipper
FROM
    customers c
        LEFT JOIN
    orders o ON c.customer_id = o.customer_id
        LEFT JOIN
    shippers sh ON o.shipper_id = sh.shipper_id
ORDER BY
    c.customer_id;
```
LEFT JOIN on customers and orders table results that all the records on customers table are included and the records that matched the condition (c.customer_id = o.customer_id) append accordingly.
The prior resulted tables now LEFT JOIN with shippers table. All the records of the prior resulted tables are included and the records that matched the condition (o.shipper_id = sh.shipper_id) appedn accordingly.

## Self Outer Join
```sql
SELECT
    e.employee_id,
    e.first_name,
    m.first_name AS manager
FROM employees e
LEFT JOIN employees m
    ON e.reports_to = m.employee_id;
```
The query above does a self outer join. Now regardless the employee has a reports_to value or not, that employee wil be included in the results and the records that matched the condition will be appended accordingly.

## The Using Clause 
When our queries get more complex, the ON cluase can get in our way of reading the query. If we have the same column name in ON clause, we can replace it with Using clause.
```sql
SELECT 
    o.order_id,
    c.first_name,
FROM orders o
JOIN customers c
    USING (customer_id)      -- It is same as 'ON o.customer_id = c.customer_id'
```

If the there are multiple same anme columns in the ON clause.
```sql
SELECT * FROM order_item
JOIN order_item_notes 
    USING(order_id, product_id)    -- It is same as 'ON order_item.order_id = order_item_notes.order_id'
```

## Natural Join (not recommand)
```sql
SELECT * FROM orders 
NATURAL JOIN customers;
```
The database will automatically join these two tables based on the columns that has the same names. 


## Cross Join
We use CROSS JOIN to join every record on the first table with every record on the second table.

Explicitly Syntax
```sql
SELECT * FROM customers c
CROSS JOIN products p
ORDER BY c.first_name;
```

Implicity Syntax
```sql
SELECT * FROM customers, orders;
```

## Union
In sql, we also can combine rows from tables (same or different). To combine two results of queries, we can use UNION operator.
```sql
SELECT -- first query
    customer_id, first_name, points, 'Bronze' AS type
FROM
    customers
WHERE
    points < 2000 
UNION SELECT -- second query
    customer_id, first_name, points, 'Sliver' AS type
FROM
    customers
WHERE
    points BETWEEN 2000 AND 3000 
UNION SELECT  -- third query
    customer_id, first_name, points, 'Gold' AS type
FROM
    customers
WHERE
    points > 3000
ORDER BY first_name;
```
Note that the number of columns that each query returns should be equal, otherwise, you will get an error and the names of the columns is determined by the first query.