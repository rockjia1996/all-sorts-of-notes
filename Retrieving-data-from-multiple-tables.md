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



