You’d like a SQL code template to reference a column from another table in a new one. This is typically done using a foreign key constraint. Here’s a professional template for creating two tables, where the second table references a column from the first:

```sql
-- Create the referenced table (parent)
CREATE TABLE users (
    id INT PRIMARY KEY,
    username VARCHAR(50) NOT NULL
);

-- Create the referencing table (child) with a foreign key
CREATE TABLE orders (
    order_id INT PRIMARY KEY,
    user_id INT,
    order_date DATE,
    FOREIGN KEY (user_id) REFERENCES users(id)
);
```

**Best Practices:**
- Ensure referenced columns are indexed (usually primary keys).
- Use appropriate data types and constraints.
- Name foreign keys clearly for maintainability.

Let me know if you need an example for a specific SQL dialect or use case!