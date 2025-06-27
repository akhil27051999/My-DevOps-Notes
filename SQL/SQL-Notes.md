# 📘 SQL Complete Notes & Cheat Sheet

## 📂 1. Create a Database in SQL

### 1.1 CREATE DATABASE: Create a New Database

```sql
CREATE DATABASE company;
```

This command creates a new database named `company`.

### 1.2 USE: Select a Specific Database to Work With

```sql
USE company;
```

This command selects the `company` database for further operations.

### 1.3 ALTER DATABASE: Modify a Database's Attributes

```sql
ALTER DATABASE database_name;
```

Modify the properties of an existing database (depends on DBMS).

### 1.4 DROP DATABASE: Delete an Existing Database

```sql
DROP DATABASE company;
```

Deletes the entire database and its contents.

---

## 🧱 2. Creating Data in SQL

### 2.1 CREATE TABLE

```sql
CREATE TABLE employees (
  employee_id INT PRIMARY KEY,
  first_name VARCHAR(50),
  last_name VARCHAR(50),
  department VARCHAR(50),
  salary DECIMAL(10, 2)
);
```

Creates a table with relevant fields and a primary key.

### 2.2 INSERT INTO

```sql
INSERT INTO employees (employee_id, first_name, last_name, department, salary)
VALUES
  (1, 'John', 'Doe', 'HR', 50000.00),
  (2, 'Jane', 'Smith', 'IT', 60000.00),
  (3, 'Alice', 'Johnson', 'Finance', 55000.00),
  (4, 'Bob', 'Williams', 'IT', 62000.00),
  (5, 'Emily', 'Brown', 'HR', 48000.00);
```

Inserts sample records into `employees`.

### 2.3 ALTER TABLE

```sql
ALTER TABLE employees ADD COLUMN new_column INT;
```

Adds a new column to the table.

### 2.4 DROP TABLE

```sql
DROP TABLE employees;
```

Deletes the table and its data.

---

## 🔍 3. Reading/Querying Data in SQL

### 3.1 SELECT

```sql
SELECT * FROM employees;
```

Fetches all records from a table.

### 3.2 DISTINCT

```sql
SELECT DISTINCT department FROM employees;
```

Returns unique department values.

### 3.3 WHERE

```sql
SELECT * FROM employees WHERE salary > 55000.00;
```

Filter rows based on a condition.

### 3.4 LIMIT

```sql
SELECT * FROM employees LIMIT 3;
```

Restrict the number of returned rows.

### 3.5 OFFSET

```sql
SELECT * FROM employees OFFSET 2;
```

Skips the first two rows.

### 3.6 FETCH

```sql
SELECT * FROM employees FETCH FIRST 3 ROWS ONLY;
```

Retrieves a specific number of rows (SQL standard).

### 3.7 CASE

```sql
SELECT first_name, last_name,
CASE
  WHEN salary > 55000 THEN 'High'
  WHEN salary > 50000 THEN 'Medium'
  ELSE 'Low'
END AS salary_category
FROM employees;
```

Adds conditional logic in results.

---

## ✏️ 4. Updating/Manipulating Data

### 4.1 UPDATE

```sql
UPDATE employees SET salary = 55000.00 WHERE employee_id = 1;
```

Modifies records.

### 4.2 DELETE

```sql
DELETE FROM employees WHERE employee_id = 5;
```

Deletes a specific row.

---

## 🔎 5. Filtering Data

### 5.1 LIKE

```sql
SELECT * FROM employees WHERE first_name LIKE 'J%';
```

Pattern match.

### 5.2 IN

```sql
SELECT * FROM employees WHERE department IN ('HR', 'Finance');
```

Checks values in a list.

### 5.3 BETWEEN

```sql
SELECT * FROM employees WHERE salary BETWEEN 50000 AND 60000;
```

Range filtering.

### 5.4 IS NULL

```sql
SELECT * FROM employees WHERE department IS NULL;
```

Checks for missing data.

### 5.5 ORDER BY

```sql
SELECT * FROM employees ORDER BY salary DESC;
```

Sort results.

---

## ⚙️ 6. SQL Operators

* **AND**:

```sql
SELECT * FROM employees WHERE department = 'IT' AND salary > 60000;
```

* **OR**:

```sql
SELECT * FROM employees WHERE department = 'HR' OR department = 'Finance';
```

* **NOT**:

```sql
SELECT * FROM employees WHERE NOT department = 'IT';
```

* **LIKE**: Pattern matching
* **IN**: Membership test
* **BETWEEN**: Range
* **IS NULL**: Null check
* **ORDER BY**: Sorting

---

## 🧲 7. Aggregation

### 7.1 COUNT

```sql
SELECT COUNT(*) FROM employees;
```

### 7.2 SUM

```sql
SELECT SUM(salary) FROM employees;
```

### 7.3 AVG

```sql
SELECT AVG(salary) FROM employees;
```

### 7.4 MIN/MAX

```sql
SELECT MIN(salary), MAX(salary) FROM employees;
```

### 7.5 GROUP BY

```sql
SELECT department, COUNT(*) FROM employees GROUP BY department;
```

### 7.6 HAVING

```sql
SELECT department, AVG(salary) FROM employees GROUP BY department HAVING AVG(salary) > 55000;
```

---

## 🛠️ 8. Constraints in SQL

### 8.1 PRIMARY KEY

```sql
CREATE TABLE employees (
  employee_id INT PRIMARY KEY,
  ...
);
```

Ensures each row is unique.

### 8.2 FOREIGN KEY

```sql
FOREIGN KEY (department_id) REFERENCES departments(department_id)
```

Links two tables together.

### 8.3 UNIQUE

```sql
email VARCHAR(100) UNIQUE
```

Ensures no duplicate values.

### 8.4 NOT NULL

```sql
first_name VARCHAR(50) NOT NULL
```

Value is required.

### 8.5 CHECK

```sql
age INT CHECK (age >= 18)
```

Validates data on insert.

---

## 📊 9. Joins in SQL

### 9.1 INNER JOIN

```sql
SELECT * FROM employees
INNER JOIN departments ON employees.department_id = departments.department_id;
```

Only matched rows from both tables.

### 9.2 LEFT JOIN

```sql
SELECT * FROM employees
LEFT JOIN departments ON employees.department_id = departments.department_id;
```

All records from left + matched records from right.

### 9.3 RIGHT JOIN

```sql
SELECT * FROM employees
RIGHT JOIN departments ON employees.department_id = departments.department_id;
```

All records from right + matched from left.

### 9.4 FULL OUTER JOIN

```sql
SELECT * FROM employees
FULL OUTER JOIN departments ON employees.department_id = departments.department_id;
```

All matched/unmatched records from both.

### 9.5 CROSS JOIN

```sql
SELECT * FROM employees
CROSS JOIN departments;
```

Cartesian product of two tables.

### 9.6 SELF JOIN

```sql
SELECT e1.first_name, e2.first_name
FROM employees e1, employees e2
WHERE e1.employee_id = e2.manager_id;
```

A table joined with itself.

---

## 🌐 10. SQL Functions

### 10.1 Scalar Functions

```sql
SELECT UPPER(first_name) FROM employees;
```

Converts text to uppercase.

### 10.2 Aggregate Functions

```sql
SELECT AVG(salary) FROM employees;
```

Calculates average.

### 10.3 String Functions

```sql
SELECT CONCAT(first_name, ' ', last_name) FROM employees;
```

Concatenate strings.

### 10.4 Date Functions

```sql
SELECT CURRENT_DATE;
```

Get today’s date.

### 10.5 Math Functions

```sql
SELECT SQRT(25);
```

Calculate square root.

---

## 📃 11. Views

### 11.1 CREATE VIEW

```sql
CREATE VIEW high_paid_employees AS
SELECT * FROM employees WHERE salary > 60000;
```

Creates a virtual table.

### 11.2 DROP VIEW

```sql
DROP VIEW IF EXISTS high_paid_employees;
```

Deletes the view.

---

## 🔢 12. Indexes

### 12.1 CREATE INDEX

```sql
CREATE INDEX idx_department ON employees(department);
```

Improves query performance.

### 12.2 DROP INDEX

```sql
DROP INDEX IF EXISTS idx_department;
```

Removes index.

---

## ✅ 13. Transactions

### 13.1 BEGIN

```sql
BEGIN TRANSACTION;
```

Start a transaction.

### 13.2 COMMIT

```sql
COMMIT;
```

Save changes.

### 13.3 ROLLBACK

```sql
ROLLBACK;
```

Undo changes.

---

## 🌟 14. Advanced SQL

### 14.1 Stored Procedures

```sql
CREATE PROCEDURE get_employee_count()
BEGIN
  SELECT COUNT(*) FROM employees;
END;
```

Reusable SQL block.

### 14.2 Triggers

```sql
CREATE TRIGGER before_insert_employee
BEFORE INSERT ON employees
FOR EACH ROW
BEGIN
  SET NEW.creation_date = NOW();
END;
```

Auto-executes logic.

### 14.3 User-defined Functions

```sql
CREATE FUNCTION calculate_bonus(salary DECIMAL)
RETURNS DECIMAL
BEGIN
  RETURN salary * 0.10;
END;
```

Custom logic as function.

### 14.4 Common Table Expressions (CTEs)

```sql
WITH high_paid AS (
  SELECT * FROM employees WHERE salary > 60000
)
SELECT * FROM high_paid;
```

Temporary named result set.
