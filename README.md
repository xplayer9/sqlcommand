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

















