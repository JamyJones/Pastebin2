Certainly! To reference a column from one table in another, you typically use a **foreign key** to establish a relationship between them. Below is a SQL template for adding a foreign key constraint to an existing table:

```sql
ALTER TABLE new_table
ADD CONSTRAINT fk_new_table_column
FOREIGN KEY (column_name)
REFERENCES existing_table(existing_column);
```

### Explanation:
- `ALTER TABLE new_table`: Modifies the new table.
- `ADD CONSTRAINT fk_new_table_column`: Adds a named foreign key constraint.
- `FOREIGN KEY (column_name)`: Specifies the column in the new table that will reference the existing table.
- `REFERENCES existing_table(existing_column)`: Defines the relationship by linking `column_name` in the new table to `existing_column` in the existing table.

#### Best Practices:
- Ensure that the `existing_column` is a **primary key** or has a **unique constraint** in the referenced table.
- Use **INDEXES** on foreign keys for optimized query performance.
- Choose appropriate **CASCADE** options (`ON DELETE CASCADE`, `ON UPDATE CASCADE`) based on how you want changes in the existing table to affect the referencing table.

Would you like assistance in optimizing constraints or handling edge cases?