

### Input -
```js
await pool.query(sqlString, arraysOfValues);
```

### Output -
```js
{
  rows: [ { id: 1, username: 'sarthak' } ],
  // 1. The actual data (Array of Objects)
  rowCount: 1,
  // 2. Total number of rows affected/returned (Number)
  command: 'SELECT'
  // 3. The type of SQL command run (String)
}
```


### returning * - for `INSERT` or `UPDATE` queries
```js
// Without RETURNING, result.rows will be empty []
postgres m kaam ho jaega but vo return automatic thodi karega, islie ->

const result = await pool.query(
  'INSERT INTO users(username) VALUES($1) RETURNING *', 
  ['sarthak']
);
// Now result.rows[0] contains the new user object with its auto-generated ID!
```


[[SQL -]]


---

## psql cmd -

```text
important ones -

database -
\l                           List all databases
\c dbname                    Switch/connect to a database

table -
\dt                          List all tables
\d tablename                 Describe a table structure
\dv                          List all views

```


```text
========================================
CONNECTING AND EXITING
========================================
psql -d dbname -U username   Connect to a database
\q                           Exit psql

========================================
DATABASE NAVIGATION
========================================
\l                           List all databases
\c dbname                    Switch/connect to a database

========================================
INSPECTING DATABASE OBJECTS
========================================
\dt                          List all tables
\d tablename                 Describe a table structure
\dv                          List all views
\dn                          List all schemas
\df                          List all functions

========================================
PERMISSIONS AND MANAGEMENT
========================================
\du                          List all database users/roles
\z                           List access privileges

========================================
INPUT, OUTPUT, AND HELP
========================================
\i filename.sql              Execute SQL commands from a file
\o filename.txt              Send query results to a file
\o                           Reset output back to screen
\e                           Open query in text editor
\?                           Show psql help
\h command                   Show SQL command help (e.g. \h SELECT)

```


---


## DDL -

```text
========================================
CREATE (Build database structures)
========================================
CREATE DATABASE name;                      Create a new database
CREATE TABLE name (col type, ...);         Create a new table
CREATE INDEX name ON tbl (col);            Create an index for performance
CREATE VIEW name AS SELECT ...;            Create a virtual table view
CREATE SCHEMA name;                        Create a database schema

========================================
ALTER (Modify existing structures)
========================================
ALTER TABLE tbl ADD COLUMN col type;       Add a new column
ALTER TABLE tbl DROP COLUMN col;           Delete a column
ALTER TABLE tbl RENAME COLUMN old TO new;  Rename a column
ALTER TABLE tbl RENAME TO new_name;        Rename a table
ALTER TABLE tbl ALTER COLUMN col SET NOT NULL; Change column constraint

========================================
DROP (Delete objects permanently)
========================================
DROP DATABASE name;                        Delete a database
DROP TABLE name;                           Delete a table and its data
DROP INDEX name;                           Delete an index
DROP VIEW name;                            Delete a view
DROP SCHEMA name;                          Delete a schema

========================================
TRUNCATE & COMMENT (Clear or document)
========================================
TRUNCATE TABLE name;                       Empty a table quickly (keep structure)
COMMENT ON TABLE name IS 'text';           Add a comment to a table

```


---


## DML -

```text
========================================
SELECT (Retrieve data)
========================================
SELECT * FROM table_name;                  Get all rows and columns
SELECT col1, col2 FROM table_name;         Get specific columns
SELECT * FROM table_name WHERE condition;  Get rows matching a condition

========================================
INSERT (Add new data)
========================================
INSERT INTO table_name (col1, col2) VALUES (val1, val2);  Insert a new row

========================================
UPDATE (Modify existing data)
========================================
UPDATE table_name SET col1 = new_val WHERE condition;     Update specific rows

========================================
DELETE (Remove data rows)
========================================
DELETE FROM table_name WHERE condition;    Delete specific rows (keeps table)

```


---

## Data Types -
1. int, double, float, decimal, serial (auto-incrementing integer)
2. varchar
3. date
4. boolean

```postgresql
decimal(5,2) --means-->  total 5 and 2 after point --like-->  46.65, 342.65,

--> 5531.67  --invalid--(as total is 6 here)

varchar(100)
date -- ese likh --> year-month-day : 2005-01-18
```

## constraints -
1. primary key
2. not null
3. default
4. unique

```postgresql
default 300
default current_date
check (length(phoneno) >= 10) --for string
check (salary >= 30000) -- for int

```

NOTE - 
- postgres auto generate name for each constraints.
- we can use contraint name to alter them (add or drop them)
- ```postgresql
--1. How to Add a Constraint
--Use `ALTER TABLE ... ADD CONSTRAINT` followed by a custom name and the constraint definition

--Check Constraint
ALTER TABLE users 
ADD CONSTRAINT age_check CHECK (age >= 18);

--Foreign Key Constraint
ALTER TABLE orders 
ADD CONSTRAINT fk_user 
FOREIGN KEY (user_id) REFERENCES users(id);

--Primary Key Constraint
ALTER TABLE products 
ADD CONSTRAINT pk_products PRIMARY KEY (product_id);
  ```

```postgresql
--2. How to Drop a Constraint
--To remove a constraint, you only need to know its exact name. Use `ALTER TABLE ... DROP CONSTRAINT`
ALTER TABLE users 
DROP CONSTRAINT age_check;


---Dropping with CASCADE:
--If another database object (like a foreign key in another table) depends on the constraint you are trying to drop, add `CASCADE` at the end to drop the dependent objects automatically
ALTER TABLE users 
DROP CONSTRAINT pk_users CASCADE;
```

```postgresql
--> To modify a constraint, drop it and add it again 
  ALTER TABLE users 
  DROP CONSTRAINT age_check,
  ADD CONSTRAINT age_check CHECK (age >= 21);

```

---


## CASE -
```postgresql
SELECT 
    product_name, 
    price,
    CASE 
        WHEN price >= 100 THEN 'Premium'
        WHEN price >= 50 AND price < 100 THEN 'Mid-range'
        ELSE 'Budget'
    END AS price_category
FROM products;

```


---

## views -
```postgresql
CREATE VIEW billing AS
(select ... whole query)

-- now i can use billing as a table form but it is not actually a table 
```

---

## roll up -
```postgresql
select
 coalesce(product,'Total'), -- jaha product column m null hoga usko replace
 sum(total_price) from billing
 group by rollup(product)
 order by sum(total_price);
```


---

## Stored routine -
- An SQL statement or a set of SQL Statement that can be stored on database server which can be call no. of times.
- it is just created one time and can be used multiple times

### 1. stored procedure -
- Set of SQL statements and procedural logic that can perform operations such as inserting, updating, deleting, and querying data.


- syntax :
```postgresql
CREATE OR REPLACE PROCEDURE procedure_name (parameter_name parameter_type, ...)
LANGUAGE plpgsql
AS $$
BEGIN
    -- procedural code here
END;
$$;
```

- eg 1:
```postgresql
CREATE OR REPLACE PROCEDURE update_emp_salary(

p_employee_id INT,

p_new_salary NUMERIC

)

LANGUAGE plpgsql

AS $$

BEGIN
 -- put your query here
UPDATE employees
SET salary = p_new_salary
WHERE emp_id = p_employee_id;

END;

$$;


-- now u can use this query multiple times like -> call update_emp_salary(p1,p2);
```

- eg 2:
```sql
CREATE OR REPLACE PROCEDURE add_employee(

p_fname VARCHAR,

p_lname VARCHAR,

p_email VARCHAR,

p_dept VARCHAR,

p_salary NUMERIC

)

LANGUAGE plpgsql

AS $$

BEGIN

INSERT INTO employees (fname, lname, email, dept, salary)

VALUES (p_fname, p_lname, p_email, p_dept, p_salary);

END;

$$;

-- now u can use this query multiple times like ->
-- call add_employee(p1,p2,p3,p4,p5);
```


---


### 2. user defined functions -
- custom function created by the user to perform specific operations and return a value.


- syntax -
```postgresql
CREATE OR REPLACE FUNCTION function_name(parameters)
RETURNS return_type AS $$
BEGIN

    -- Function body (SQL statements)

    RETURN some_value; -- For scalar functions

END;
$$ LANGUAGE plpgsql;
```


Q: Find name of the employees in each department having maximum salary.

```postgresql
CREATE OR REPLACE FUNCTION dept_max_sal_emp1(dept_name VARCHAR)

RETURNS TABLE(emp_id INT, fname VARCHAR, salary NUMERIC)

AS $$

BEGIN

RETURN QUERY

SELECT

e.emp_id, e.fname, e.salary

FROM

employees e

WHERE

e.dept = dept_name

AND e.salary = (

SELECT MAX(emp.salary)

FROM employees emp

WHERE emp.dept = dept_name

);

END;

$$ LANGUAGE plpgsql;


--call like query ->
select * from dept_max_sal_emp1('IT');
select * from dept_max_sal_emp1('HR');
select * from dept_max_sal_emp1('finance');
```


---



## Windows function -
- Window functions, also known as analytic functions allow you to perform calculations across a set of rows related to the current row.
- Defined by an OVER() clause.
- some windows functions are:

- ROW_NUMBER()
    
- RANK()
    
- DENSE_RANK()
    
- LAG()
    
- LEAD()


Q: running sum.
```postgresql
select name, salary,
sum(salary) over(order by salary)
from employees;
```

Q: row number.
```postgresql
select fname, dept, salary,
       ROW_NUMBER()
       OVER(PARTITION BY dept ORDER BY salary DESC)
       AS row_num
from employees;
```


---


## CTE (Common Table Expression) -
CTE is a temporary result set that you can define within a query to simplify complex SQL statements.

- syntax -
```postgresql
WITH cte_name (optional_column_list) AS (
    -- CTE query definition
    SELECT ...
)
-- Main query referencing the CTE (use)
SELECT ...
FROM cte_name
WHERE ...;
```