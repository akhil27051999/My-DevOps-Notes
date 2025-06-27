# 📘 SQL Queries for Interviews

1. **What is the difference between `WHERE` and `HAVING` clause?**

* `WHERE` filters rows before aggregation.
* `HAVING` filters groups after aggregation.

2. **What are different types of joins in SQL?**

* `INNER JOIN`, `LEFT JOIN`, `RIGHT JOIN`, `FULL OUTER JOIN`, `CROSS JOIN`, `SELF JOIN`

3. **Explain `INNER JOIN` vs `LEFT JOIN` with an example.**

```sql
-- INNER JOIN: only matching rows
SELECT u.name, o.order_id FROM users u
INNER JOIN orders o ON u.id = o.user_id;

-- LEFT JOIN: all from left, NULLs for unmatched right
SELECT u.name, o.order_id FROM users u
LEFT JOIN orders o ON u.id = o.user_id;
```

4. **Write a query to find the second highest salary from employees.**

```sql
SELECT MAX(salary) FROM employees
WHERE salary < (SELECT MAX(salary) FROM employees);
```

5. **How do you remove duplicate rows from a table?**

```sql
DELETE FROM employees
WHERE id NOT IN (
  SELECT MIN(id) FROM employees GROUP BY email
);
```

6. **How to find the number of orders placed by each customer?**

```sql
SELECT customer_id, COUNT(*) AS order_count
FROM orders
GROUP BY customer_id;
```

7. **How to select only even-numbered rows in PostgreSQL?**

```sql
SELECT * FROM (
  SELECT *, ROW_NUMBER() OVER () AS rn FROM users
) AS sub
WHERE rn % 2 = 0;
```

8. **Difference between `UNION` and `UNION ALL`?**

* `UNION`: removes duplicates.
* `UNION ALL`: keeps duplicates.

9. **How to find customers with no orders?**

```sql
SELECT name FROM customers c
LEFT JOIN orders o ON c.id = o.customer_id
WHERE o.id IS NULL;
```

10. **GROUP BY vs PARTITION BY?**

* `GROUP BY`: aggregates data into rows.
* `PARTITION BY`: used with window functions, does not reduce row count.

11. **Write a query to find employees who earn more than their manager.**

```sql
SELECT e.name FROM employees e
JOIN employees m ON e.manager_id = m.id
WHERE e.salary > m.salary;
```

12. **What is a subquery? Provide an example.**

```sql
SELECT name FROM employees
WHERE salary > (SELECT AVG(salary) FROM employees);
```

13. **What is a CTE (Common Table Expression)?**

```sql
WITH top_earners AS (
  SELECT * FROM employees WHERE salary > 100000
)
SELECT * FROM top_earners;
```

14. **What are window functions?**
    They perform calculations across a set of table rows related to the current row.

```sql
SELECT name, salary, RANK() OVER (ORDER BY salary DESC) AS rank
FROM employees;
```

15. **Find the department with the highest average salary.**

```sql
SELECT department FROM employees
GROUP BY department
ORDER BY AVG(salary) DESC
LIMIT 1;
```

16. **Write a query to retrieve the third highest salary.**

```sql
SELECT salary FROM (
  SELECT salary, DENSE_RANK() OVER (ORDER BY salary DESC) AS rnk
  FROM employees
) AS ranked
WHERE rnk = 3;
```

17. **Difference between `RANK()`, `DENSE_RANK()`, and `ROW_NUMBER()`?**

* `RANK()`: skips numbers if there's a tie.
* `DENSE_RANK()`: no gaps.
* `ROW_NUMBER()`: unique row index.

18. **How to update a column based on another table?**

```sql
UPDATE orders o
SET total = i.amount
FROM invoices i
WHERE o.invoice_id = i.id;
```

19. **What is normalization? Explain 1NF, 2NF, 3NF.**

* 1NF: Atomic values
* 2NF: No partial dependency
* 3NF: No transitive dependency

20. **What is denormalization?**
    The process of introducing redundancy to improve performance.

21. **What is an index? How does it improve performance?**
    An index speeds up data retrieval but may slow down inserts/updates.

```sql
CREATE INDEX idx_email ON users(email);
```

22. **What is a composite key?**
    A primary key composed of multiple columns.

23. **How to find duplicate email entries in a user table?**

```sql
SELECT email, COUNT(*) FROM users
GROUP BY email
HAVING COUNT(*) > 1;
```

24. **How to retrieve the last 5 inserted records?**

```sql
SELECT * FROM users ORDER BY created_at DESC LIMIT 5;
```

25. **What is a transaction? Explain ACID properties.**

* **Atomicity**: All-or-nothing
* **Consistency**: Valid state transitions
* **Isolation**: Transactions don’t interfere
* **Durability**: Changes persist after commit

26. **Difference between DELETE, TRUNCATE, DROP?**

* `DELETE`: removes rows
* `TRUNCATE`: faster, removes all rows
* `DROP`: deletes the entire table

27. **What is the use of the `EXPLAIN` keyword?**
    Used to view the query execution plan.

```sql
EXPLAIN SELECT * FROM users WHERE age > 30;
```

28. **What is a view?**
    A virtual table based on the result-set of an SQL statement.

```sql
CREATE VIEW active_users AS SELECT * FROM users WHERE status = 'active';
```

29. **Difference between View and Materialized View?**

* View: Logical, no data stored
* Materialized View: Stores query result

30. **Write a query to get user count per country.**

```sql
SELECT country, COUNT(*) FROM users GROUP BY country;
```

31. **What are NULLs in SQL?**
    Unknown/missing values. Use `IS NULL` / `IS NOT NULL`.

32. **Query to replace NULLs with default value**

```sql
SELECT COALESCE(phone, 'N/A') FROM users;
```

33. **What is the purpose of `DISTINCT`?**
    Removes duplicate rows.

34. **Write a query to list all employees and their manager names.**

```sql
SELECT e.name, m.name AS manager
FROM employees e
LEFT JOIN employees m ON e.manager_id = m.id;
```

35. **Difference between CHAR and VARCHAR?**

* `CHAR(n)`: Fixed length
* `VARCHAR(n)`: Variable length

36. **What are triggers?**
    Procedures triggered automatically in response to certain events on a table.

37. **Find average salary per department.**

```sql
SELECT department, AVG(salary)
FROM employees
GROUP BY department;
```

38. **Find employees who joined in the last 30 days.**

```sql
SELECT * FROM employees
WHERE join_date >= CURRENT_DATE - INTERVAL '30 days';
```

39. **Write a query using `CASE` statement.**

```sql
SELECT name,
CASE 
  WHEN salary >= 100000 THEN 'High'
  WHEN salary >= 50000 THEN 'Medium'
  ELSE 'Low'
END AS category
FROM employees;
```

40. **What is a surrogate key?**
    A system-generated unique identifier (e.g., auto-increment ID).

41. **What is referential integrity?**
    Ensures that foreign keys match primary keys in referenced tables.

42. **Query to delete all employees from Sales dept.**

```sql
DELETE FROM employees WHERE department = 'Sales';
```

43. **What is a schema?**
    Logical structure of the database, like a folder.

44. **How to count total number of rows in a table?**

```sql
SELECT COUNT(*) FROM table_name;
```

45. **Query to get department-wise highest paid employee.**

```sql
SELECT * FROM (
  SELECT *, ROW_NUMBER() OVER (PARTITION BY department ORDER BY salary DESC) as rn
  FROM employees
) AS ranked
WHERE rn = 1;
```

46. **How to paginate results in SQL?**

```sql
SELECT * FROM products LIMIT 10 OFFSET 20;
```

47. **How to extract year from a date column?**

```sql
SELECT EXTRACT(YEAR FROM created_at) FROM orders;
```

48. **What is the default sorting order in SQL?**
    Ascending (`ASC`)

49. **Difference between BETWEEN and IN operator?**

* `BETWEEN`: range check
* `IN`: list of values

50. **Query to find users whose name starts with 'A'**

```sql
SELECT * FROM users WHERE name LIKE 'A%';
```

51. **How to find the nth highest salary using subquery?**

```sql
SELECT salary FROM employees e1
WHERE N-1 = (
  SELECT COUNT(DISTINCT salary) FROM employees e2
  WHERE e2.salary > e1.salary
);
```

52. **What are some common SQL performance optimizations?**

* Use indexes
* Avoid SELECT \*
* Analyze query with EXPLAIN
* Avoid correlated subqueries

53. **Difference between clustered and non-clustered index?**

* Clustered: rearranges table
* Non-clustered: separate structure

54. **What is a foreign key constraint?**
    A column that references another table’s primary key to enforce relationships.

55. **What is the difference between logical and physical data independence?**

* Logical: changing schema without affecting applications
* Physical: changing storage without affecting schema
