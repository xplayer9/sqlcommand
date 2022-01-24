# sqlcommand

```SQL
SELECT name
FROM customers;
```

```SQL
SELECT * 
FROM customers;
```

- return only rows with a unique name from the customers table
```SQL
SELECT DISTINCT name
FROM customers;
```

- SELECT INTO copies the specified data from one table into another
```SQL
SELECT * INTO customers
FROM customers_backup;
```

SELECT TOP only returns the top x number or percent from a table
```SQL
SELECT TOP 50 * FROM customers;
```
```SQL
SELECT TOP 50 PERCENT * FROM customers;
```

- AS renames a column or table with an alias
```SQL
SELECT name AS first_name
FROM customers;
```

- WHERE filters your query to only return results that match a set condition. Conditional operators like =, >, <, >=, <=, etc.
```SQL
SELECT name
FROM customers
WHERE name = ‘Bob’;
```

- AND/OR combines two or more conditions in a single query. 
```SQL
SELECT name
FROM customers
WHERE name = ‘Bob’ AND age = 55;
```
- BETWEEN filters your query to return only results that fit a specified range
```SQL
SELECT name
FROM customers
WHERE age BETWEEN 45 AND 55;
```


- LIKE searches for a specified pattern in a column
```SQL
SELECT name
FROM customers
WHERE name LIKE ‘%Bob%’;
```
```
%x — will select all values that begin with x
%x% — will select all values that include x
x% — will select all values that end with x
x%y — will select all values that begin with x and end with y
_x% — will select all values have x as the second character
x_% — will select all values that begin with x and are at least two characters long
```

- IN allows us to specify multiple values we want to select
```SQL
SELECT name
FROM customers
WHERE name IN (‘Bob’, ‘Fred’, ‘Harry’);
```

- IS NULL/IS NOT NULL will return only rows with a NULL/NOT NULL value
```SQL
SELECT name
FROM customers
WHERE name IS NULL;
```

- CREATE TABLE creates a new table inside a database
```SQL
CREATE TABLE customers (
    customer_id int,
    name varchar(255),
    age int
);
```
- CREATE INDEX generates an index for a table. Indexes are used to retrieve data from a database faster.
```SQL
CREATE INDEX idx_name
ON customers (name);
```

- CREATE VIEW creates a virtual table based on the result set of an SQL statement. A view is like a regular table, but it is not saved as a permanent table in the database
```SQL
CREATE VIEW [Bob Customers] AS
SELECT name, age
FROM customers
WHERE name = ‘Bob’;
```
- DROP TABLE/INDEX deletes a table/index
```SQL
DROP TABLE customers;
```

--- UPDATE statement is used to update data in a table
```SQL
UPDATE customers
SET age = 56
WHERE name = ‘Bob’;
```

- DELETE can remove all rows from a table
```SQL
DELETE FROM customers
WHERE name = ‘Bob’;
```

- ALTER TABLE allows you to add or remove columns from a table
```SQL
ALTER TABLE customers
ADD surname varchar(255);
```
```SQL
ALTER TABLE customers
DROP COLUMN surname;
```

### AGGREGATE FUNCTIONS (COUNT/SUM/AVG/MIN/MAX)
- COUNT/SUM/AVG/MIN/MAX returns the number of rows that match the specified criteria
```SQL
SELECT COUNT(*)
FROM customers;
```

- GROUP BY statement groups rows with the same values into summary rows
- For example, the code below will display the average age for each name that appears in our customers table
```SQL
SELECT name, AVG(age)
FROM customers
GROUP BY name;
```

- HAVING performs the same action as the WHERE clause. The difference is that HAVING is used for aggregate functions, whereas WHERE doesn’t work with them
- The below example would return the number of rows for each name, but only for names with more than 2 records.
```
SELECT COUNT(customer_id), name
FROM customers
GROUP BY name
HAVING COUNT(customer_id) > 2;
```

- ORDER BY sets the order of the returned results. The order will be ascending by default.
```SQL
SELECT name
FROM customers
ORDER BY age;
```

- DESC will return the results in descending order.
```SQL
SELECT name
FROM customers
ORDER BY age DESC;
```

- The OFFSET statement works with ORDER BY and specifies the number of rows to skip
```SQL
SELECT name
FROM customers
ORDER BY age
OFFSET 10 ROWS;
```

- FETCH specifies the number of rows to return after the OFFSET clause has been processed
```SQL
SELECT name
FROM customers
ORDER BY age
OFFSET 10 ROWS
FETCH NEXT 10 ROWS ONLY;
```

## JOINS (INNER, LEFT, RIGHT, FULL)
INNER JOIN selects records that have matching values in both tables.
```SQL
SELECT name
FROM customers
INNER JOIN orders
ON customers.customer_id = orders.customer_id;
```
- LEFT JOIN selects records from the left table that match records in the right table. In the below example the left table is customers.
```SQL
SELECT name
FROM customers
LEFT JOIN orders
ON customers.customer_id = orders.customer_id;
```

- RIGHT JOIN selects records from the right table that match records in the left table. In the below example the right table is orders.
```SQL
SELECT name
FROM customers
RIGHT JOIN orders
ON customers.customer_id = orders.customer_id;
```

- FULL JOIN selects records that have a match in the left or right table. Think of it as the “OR” JOIN compared with the “AND” JOIN (INNER JOIN).
```SQL
SELECT name
FROM customers
FULL OUTER JOIN orders
ON customers.customer_id = orders.customer_id;
```

- EXISTS is used to test for the existence of any record in a subquery.
```
SELECT name
FROM customers
WHERE EXISTS
(SELECT order FROM ORDERS WHERE customer_id = 1);
```

- GRANT gives a particular user access to database objects such as tables, views or the database itself. The below example would give SELECT and UPDATE access on the customers table to a user named “usr_bob”.
```SQL
GRANT SELECT, UPDATE ON customers TO usr_bob;
```

- REVOKE removes a user’s permissions for a particular database object.
```SQL
REVOKE SELECT, UPDATE ON customers FROM usr_bob;
```

- SAVEPOINT allows you to identify a point in a transaction to which you can later roll back. Similar to creating a backup
```SQL
SAVEPOINT SAVEPOINT_NAME;
```

- COMMIT is for saving every transaction to the database
- A COMMIT statement will release any existing savepoints that may be in use and once the statement is issued, you cannot roll back the transaction.
```SQL
DELETE FROM customers
WHERE name = ‘Bob’;
COMMIT
```

- ROLLBACK is used to undo transactions which are not saved to the database
``` SQL
ROLLBACK TO SAVEPOINT_NAME;
```

- TRUNCATE TABLE removes all data entries from a table in a database, but keeps the table and structure in place. Similar to DELETE.
```SQL
TRUNCATE TABLE customers;
```

- UNION combines multiple result-sets using two or more SELECT statements and eliminates duplicate rows.
```SQL
SELECT name FROM customers UNION SELECT name FROM orders;
```

- UNION ALL combines multiple result-sets using two or more SELECT statements and keeps duplicate rows.
```SQL
SELECT name FROM customers UNION ALL SELECT name FROM orders;
```













