# Database Cheat Sheet

## Relational Databases

### Key Concepts
- **Joins**: Combine tables with `INNER JOIN`, `LEFT JOIN`, `RIGHT JOIN`, and `FULL OUTER JOIN`.
- **Subqueries**: Nest queries; correlated subqueries depend on the outer query.
- **CTEs**: Use `WITH` for temporary result sets in complex queries.
- **Window Functions**: Perform analytics with `ROW_NUMBER()`, `RANK()`, etc.
- **Aggregation**: Summarize data with `GROUP BY` and filter with `HAVING`.
- **Conditional Logic**: Use `CASE` for conditional query outputs.

### Design Principles
- **ERDs**: Visualize tables and their relationships.
- **Normalization**: Apply 1NF, 2NF, 3NF to eliminate redundancy.
- **Denormalization**: Optimize for speed by combining tables where needed.

---

## Indexing and Optimization

### Indexing
- **Clustered**: Data is stored in table order.
- **Non-clustered**: Separate storage for faster lookups.
- **Composite**: Index on multiple columns for complex queries.

### Optimization Tips
- Analyze query execution plans.
- Avoid `SELECT *`; fetch only necessary columns.
- Batch operations to prevent `N+1` query issues.

---

## Transactions and Concurrency

### Transactions
- **ACID**: Ensure data reliability (Atomicity, Consistency, Isolation, Durability).
- Use `ROLLBACK` to undo failed transactions.

### Concurrency Control
- Implement locking mechanisms to avoid conflicts.
- Use appropriate isolation levels (`READ COMMITTED`, `SERIALIZABLE`, etc.).

---

## NoSQL Databases

### Types
- **Key-Value**: Simple lookups (e.g., Redis).
- **Document**: JSON-like data (e.g., MongoDB).
- **Column-Family**: Analytical use (e.g., Cassandra).
- **Graph**: Relationship-heavy data (e.g., Neo4j).

### Examples
- **MongoDB**: Perform CRUD and aggregations.
- **Redis**: Cache session data for performance.

---

## Advanced Topics

### Backup & Recovery
- **Strategies**: Full, differential, incremental backups.
- **Recovery**: Point-in-time restores for minimal data loss.

### Security
- Use roles and privileges to control access.
- Encrypt data at rest and in transit.
- Prevent SQL injection with parameterized queries.

### Performance Tuning
- **Partitioning**: Split tables for better performance.
- **Sharding**: Distribute data horizontally across servers.
- **Caching**: Reduce load with query caching.

---

## Quick SQL Examples

### Basic Queries
```sql
SELECT name, age FROM users WHERE age > 21;
```

### Joins
```sql
SELECT orders.id, users.name
FROM orders
INNER JOIN users ON orders.user_id = users.id;
```

### Aggregation
```sql
SELECT department, COUNT(*)
FROM employees
GROUP BY department;
```

### Window Functions
```sql
SELECT name, salary, RANK() OVER (ORDER BY salary DESC) AS rank
FROM employees;
```

---

## Recommended Tools
- **PostgreSQL**: Advanced relational database features.
- **MongoDB**: Flexible document-oriented database.
- **Redis**: Lightning-fast key-value store.
- **MySQL Workbench**: Visual schema design.

---
