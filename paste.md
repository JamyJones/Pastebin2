In PostgreSQL (and by extension Supabase), when referencing columns with spaces in their names, you need to escape the column name using double quotes `"`. 

### How to reference a column with spaces:
Suppose you have a column `"Created at"` in the `auth.users` table, and you want to select or filter based on it.

### Example: Selecting data
```sql
SELECT 
  id,
  email,
  "Created at"
FROM auth.users;
```

### Example: Filtering based on the `"Created at"` column
```sql
SELECT 
  id,
  email
FROM auth.users
WHERE "Created at" > '2023-01-01';
```

### Reference a specific column value (e.g., to join or insert):
If you're referencing this column in other tables or operations, always enclose the column name in double quotes:

```sql
-- Example: inserting into another table, referencing "Created at"
INSERT INTO events (user_id, event_time)
SELECT 
  id,
  "Created at"
FROM auth.users
WHERE email = 'example@example.com';
```

### Important notes:
- **Consistency:** Always double-quote column names with spaces when used in SQL statements.
- **Best practice:** It’s generally recommended to avoid spaces in column names for simplicity, but if you're working with existing schema, quoting is necessary.

---

If you need to alias this column in a query:
```sql
SELECT 
  id,
  email,
  "Created at" AS created_at
FROM auth.users;
```

This will allow you to refer to `"Created at"` as `created_at` in the result set.

---

### Summary
- Use double quotes `"Created at"` to reference the column.
- Be consistent in quoting for select, insert, update, delete operations referencing such columns.

Let me know if you'd like an example with a specific use case!