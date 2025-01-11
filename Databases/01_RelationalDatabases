# Database Cheat Sheet

## Relational Databases

### Key Concepts

- **Joins**: Combine data from multiple tables based on related columns.
  - **INNER JOIN**: Returns rows with matching values in both tables.
    ```sql
    SELECT orders.id, customers.name
    FROM orders
    INNER JOIN customers ON orders.customer_id = customers.id;
    ```
  - **LEFT JOIN**: Returns all rows from the left table, and matching rows from the right table. If no match, NULL is returned.
    ```sql
    SELECT employees.name, departments.department_name
    FROM employees
    LEFT JOIN departments ON employees.department_id = departments.id;
    ```
  - **RIGHT JOIN**: Similar to LEFT JOIN, but returns all rows from the right table.
  - **FULL OUTER JOIN**: Returns rows when there is a match in either table.

- **Subqueries**: A query nested inside another query.
  - Example: Get employees earning above the average salary.
    ```sql
    SELECT name
    FROM employees
    WHERE salary > (SELECT AVG(salary) FROM employees);
    ```

- **CTEs (Common Table Expressions)**: Temporary named result sets.
  - Example: Use `WITH` to simplify complex queries.
    ```sql
    WITH SalesCTE AS (
        SELECT salesperson_id, SUM(sales_amount) AS total_sales
        FROM sales
        GROUP BY salesperson_id
    )
    SELECT * FROM SalesCTE WHERE total_sales > 10000;
    ```

- **Window Functions**: Perform calculations across a set of rows related to the current row.
  - Example: Rank employees by salary within departments.
    ```sql
    SELECT name, department_id, salary,
           RANK() OVER (PARTITION BY department_id ORDER BY salary DESC) AS rank
    FROM employees;
    ```

- **Aggregation**: Summarize data with `GROUP BY` and filter results with `HAVING`.
  - Example: Count employees per department.
    ```sql
    SELECT department_id, COUNT(*) AS employee_count
    FROM employees
    GROUP BY department_id;
    ```

- **Conditional Logic**: Apply conditions within queries using `CASE`.
  - Example: Label employees as "High" or "Low" earners based on salary.
    ```sql
    SELECT name,
           CASE
               WHEN salary > 50000 THEN 'High'
               ELSE 'Low'
           END AS salary_category
    FROM employees;
    ```

### Design Principles

- **Entity-Relationship Diagrams (ERDs)**:
  - Visualize tables, columns, and relationships (e.g., one-to-many, many-to-many).
  - Example tools: Lucidchart, dbdiagram.io.

- **Normalization**: Structure databases to reduce redundancy and improve consistency.
  - **1NF**: Eliminate repeating groups; ensure atomicity.
  - **2NF**: Remove partial dependencies (all non-key attributes depend on the entire primary key).
  - **3NF**: Remove transitive dependencies (non-key attributes depend only on the primary key).

- **Denormalization**: Optimize read performance by combining tables or duplicating data.
  - Trade-off: Increases redundancy and may require more maintenance.

---

Use this section to understand and quickly reference essential concepts and operations in relational databases!
