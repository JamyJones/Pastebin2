In PostgreSQL, you can achieve ranking of rows based on a column using the `RANK()`, `DENSE_RANK()`, or `ROW_NUMBER()` window functions. These functions allow you to assign a rank to each row based on the values in a specified column, such as your "points" column.

Here’s how you can do it:

1. **Using `RANK()`**: This function assigns a unique rank to each distinct value in the specified column, with gaps in the ranking for ties.

2. **Using `DENSE_RANK()`**: This function also assigns a unique rank to each distinct value, but it does not leave gaps in the ranking for ties.

3. **Using `ROW_NUMBER()`**: This function assigns a unique sequential integer to rows, regardless of ties.

Here’s an example SQL query that demonstrates how to use `RANK()` to assign positions based on the "points" column:

```sql
WITH RankedPoints AS (
    SELECT 
        points,
        RANK() OVER (ORDER BY points DESC) AS position
    FROM 
        your_table_name
)
UPDATE your_table_name
SET position = RankedPoints.position
FROM RankedPoints
WHERE your_table_name.points = RankedPoints.points;
```

### Explanation:
- The `WITH` clause creates a Common Table Expression (CTE) named `RankedPoints` that selects the `points` and calculates the rank based on the `points` column in descending order.
- The `UPDATE` statement then updates the `position` column in your original table with the calculated ranks from the CTE.

Make sure to replace `your_table_name` with the actual name of your table.

### Note:
- If you want to avoid gaps in the ranking for ties, you can replace `RANK()` with `DENSE_RANK()`.
- If you want each row to have a unique position regardless of ties, use `ROW_NUMBER()`.