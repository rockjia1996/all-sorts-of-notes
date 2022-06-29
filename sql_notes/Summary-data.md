# Summary Data

## Aggregate Functions
MAX() 
MIN()
AVG()
SUM()
COUNT()

```sql
SELECT  
    MAX(invoice_total) as highest,
    MIN(invoice_total) as lowest,
    AVG(invoice_total) as average,
    SUM(invoice_total) as total,
    COUNT(invoice_total) as number_of_invoices
FROM invoices;
```

Note that COUNT() will count the duplicated values. To get the unique value, we can use DISTINCT keyword:
```sql
SELECT COUNT(DISTINCT client_id) FROM invoices;
```

## The GROUP BY Clause
GROUP BY group data by one or more columns 
```sql
SELECT 
    client_id,
    SUM(invoice_total) as total_sales
FROM invoices
WHERE invoice_datre >= "2019-07-01"
GROUP BY client_id
ORDER BY total_sales BY DESC;
```
The order of the clause is the following
SELECT > FROM > JOIN > WHERE > GROUP BY > HAVING > ORDER BY

To group with mulitiple columns
```sql
SELECT p.date, pm.name, SUM (amount)
FROM 
    payments p
    JOIN
    payment_methods pm
    ON
    p.payment_id = pm.payment_method_id
GROUP BY
    p.date, name;
```

## HAVING Clause
We use HAVING clause to filter data after the GROUP BY clause
```sql
SELECT client_id, SUM(invoice_total) AS total_sales
FROM invoice -- can't use WHERE total_sales > 500 clause we haven't GROUP the client_id
GROUP BY client_id
HAVING total_sales > 500;
```
To solve the problem of the shown case, HAVING is declared after GROUP BY.
Note that HAVING clause only accepts teh columns that are selected in SELECT clause.

Example
```sql
SELECT c.customer_id, c.state, SUM(oi.unit_price * oi.quantity)
AS total
FROM 
    order_item oi JOIN orders o ON o.order_id = oi.order_id
                  Join customers c ON c.customer_id = o.customer_id
GROUP BY c.customer_id
HAVING c.state = "VA" AND total > 100;
```

## The ROLLUP Operator
The ROLLUP() summarize the entire column. The opeator is MySQL specific.
```sql
SELECT client_id, SUM(invoice_total) as total_sales
FROM invoices
GROUP BY client_id WITH ROLLUP
```








