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

## 🧮 7. Aggregation

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

✅ *To be continued with*: Constraints, Joins, Functions, Views, Indexes, Transactions, Advanced Queries

Would you like me to continue the rest of the SQL notes into this README format?
