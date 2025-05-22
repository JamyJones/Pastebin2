To assign ranking positions to rows in PostgreSQL based on a specific column, you can use the window function ROW_NUMBER(). This function assigns a unique sequential integer to rows within a result set, ordered by the specified column.

**Example:**  
Suppose you have a table scores with columns id, name, and points. To rank users by their points (highest first):

```sql
SELECT
  id,
  name,
  points,
  ROW_NUMBER() OVER (ORDER BY points DESC) AS rank
FROM
  scores;
```

**Best Practices:**

- Use ORDER BY inside the OVER clause to specify the ranking criteria.
- If you want to handle ties (same points get the same rank), use RANK() or DENSE_RANK() instead of ROW_NUMBER().
- Always specify the ordering direction (ASC or DESC) for clarity.

**Handling Ties Example:**

```sql
SELECT
  id,
  name,
  points,
  RANK() OVER (ORDER BY points DESC) AS rank
FROM
  scores;
```

Let me know if you need more details or examples for your specific use case.