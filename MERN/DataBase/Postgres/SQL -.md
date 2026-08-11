


#### Key Points -
- inner join = join
- it is not compulsory to have / use primary and foreign keys to join them







The default port for **MySQL** is:
## **3306**
----

### **Quick Facts About the MySQL Port:**

- **Protocol:** It uses **TCP** (Transmission Control Protocol) for database connections.
    
- **Secure/Encrypted Port:** MySQL also uses port **33060** for the MySQL X Protocol (used for newer features like the X DevAPI and document store features).


-----



#### Q1. Get tweets only containing more than 4 letter 'a' in it -

1. Manual trick -
```sql
SELECT tweet_id 
FROM Tweets 
WHERE LENGTH(content) - LENGTH(REPLACE(LOWER(content), 'a', '')) > 4;
```

2. Using regex -> regular expression
```sql
SELECT tweet_id 
FROM Tweets 
WHERE content REGEXP '(.*a.*){5,}';

/*
### 1. The Core Piece: `.*a.*`

- `a` : This just matches the literal letter 'a'.
    
- `.` (Dot) : This is a wildcard. It means **"any character"** (a letter, a number, a space, a symbol).
    
- `*` (Asterisk) : This means **"zero or more times"**.
    
- **Put together (`.*a.*`)**: This means _"find a letter 'a' that can have absolutely anything (or nothing) before it, and absolutely anything (or nothing) after it."_ Essentially, it just means **"find a section of text that contains at least one 'a'"**.
    

### 2. The Grouping: `(...)`

- The parentheses group everything inside them together as a single unit.
    
- So, `(.*a.*)` tells the computer to look for that entire "text containing an 'a'" block as a single entity.
    

### 3. The Multiplier: `{5,}`

- Curly braces `{}` are used for counting repetitions.
    
- `{5}` would mean exactly 5 times.
    
- `{5,}` (with the comma) means **"5 or more times"** (at least 5, but could be more).
*/
```


#### Date difference -
```sql
datediff(w1.recordDate, w2.recordDate) = 1
or
subdate(w1.recordDate, 1) = w2.recordDate
```


### Group By -
- whole select columns as it is
- can use 1,2,3 -  in seq
- ```sql
  SELECT stu.student_id, stu.student_name, sub.subject_name,

count(e.subject_name) as attended_exams

FROM Students stu

JOIN Subjects sub

LEFT JOIN Examinations e

ON stu.student_id = e.student_id

AND sub.subject_name = e.subject_name

GROUP BY 1,2,3

ORDER BY 1,3;
  ```




----------------

#### Group By v/s Where -
Ah, the classic `HAVING` vs. `WHERE` trap! It catches almost everyone at some point.

The error `Unknown column 't.transaction_id' in 'having clause'` is happening because of the **SQL Order of Execution**.

When SQL runs your query, it groups the rows using `GROUP BY v.customer_id` _before_ it evaluates the `HAVING` clause. Once the rows are grouped by `customer_id`, the individual rows from the `Transactions` table (like `t.transaction_id`) are bundled up. Because `t.transaction_id` isn't in your `SELECT` list or wrapped in an aggregate function (like `COUNT()` or `SUM()`), SQL loses track of it by the time it reaches the `HAVING` step.

### The Fix

To filter out the visits that didn't result in a transaction, you should use a **`WHERE`** clause instead. `WHERE` filters the rows _before_ they get grouped together, meaning SQL knows exactly what `t.transaction_id` is.

Here is how you should update your code:

SQL

```sql
SELECT 
    v.customer_id, 
    COUNT(v.customer_id) AS count_no_trans 
FROM Visits v 
LEFT JOIN Transactions t 
    ON v.visit_id = t.visit_id 
WHERE t.transaction_id IS NULL  -- Filter BEFORE grouping
GROUP BY v.customer_id;
```


----


### Order of Execution -

```sql
-- Complete SELECT query

SELECT DISTINCT column, AGG_FUNC(_column_or_expression_), …
FROM mytable 
	JOIN another_table 
		ON mytable.column = another_table.column 
WHERE _constraint_expression_ 
GROUP BY column 
	HAVING _constraint_expression_ 
ORDER BY _column_ ASC/DESC
LIMIT _count_ OFFSET _COUNT_;
```

1. FROM
2. JOIN
3. WHERE
4. GROUP BY
5. HAVING
6. SELECT
7. DISTINCT
8. ORDER BY
9. LIMIT / OFFSET

---

## Important functions -

Here is the categorization of all essential SQL functions, broken down by their core architectural behavior.

### 1. Scalar Functions (Single-Row Functions)

These functions process individual values from a single row and return exactly one output per row.

- **String / Text**
    - `UPPER(str)` / `LOWER(str)`: Changes text case.
    - `TRIM(str)`: Removes leading and trailing spaces.
    - `SUBSTRING(str, start, len)`: Extracts a portion of text.
    - `CONCAT(str1, str2)`: Joins two or more strings together.
    - `LENGTH(str)` / `LEN(str)`: Counts characters in a string.
    - `REPLACE(str, old, new)`: Swaps specific characters. 
- **Numeric / Math**
    - `ROUND(num, places)`: Rounds a number to specified decimals.
    - `ABS(num)`: Returns the absolute (positive) value.
    - `CEIL(num)` / `FLOOR(num)`: Rounds up or down to the nearest integer.
    - `MOD(dividend, divisor)`: Returns the remainder of a division. 
- **Date / Time**
    - `NOW()` / `CURRENT_TIMESTAMP`: Returns the current date and time.
    - `EXTRACT(part FROM date)` / `DATE_PART()`: Pulls components like year, month, or day.
    - `DATE_ADD(date, interval)` / `DATEADD()`: Adds time to a date.
    - `DATEDIFF(end, start)`: Calculates the time difference between two dates. 
- **Conditional / Logical**
    - `COALESCE(val1, val2, ...)`: Returns the first non-null value in a list.
    - `IFNULL(val, default)` / `ISNULL()`: Replaces null values with a specified alternative.
    - `CAST(val AS type)` / `CONVERT()`: Changes the data type of a value. 

---

### 2. Aggregate Functions (Group Functions)

These functions look across multiple rows of data to calculate a single summary result. They are almost always paired with a `GROUP BY` clause. 
- `COUNT(column)`: Counts the number of rows or non-null values.
- `SUM(column)`: Adds up all numeric values in a column.
- `AVG(column)`: Calculates the mathematical average of a column.
- `MIN(column)` / `MAX(column)`: Finds the lowest or highest value in a group. 

---

### 3. Window Functions (Analytic Functions)

These functions perform calculations across a set of rows (a "window") that are related to the current row. Unlike aggregate functions, they do not collapse your rows into a single summary output. 
- **Ranking**
    - `ROW_NUMBER()`: Assigns a unique sequential integer to each row.
    - `RANK()`: Assigns ranks, leaving gaps if there are ties.
    - `DENSE_RANK()`: Assigns ranks without leaving any gaps for ties. 
- **Value / Navigation**
    - `LAG(column, offset)`: Fetches a value from a previous row.
    - `LEAD(column, offset)`: Fetches a value from a subsequent row.
    - `FIRST_VALUE(column)` / `LAST_VALUE(column)`: Retrieves the first or last value in the window. 