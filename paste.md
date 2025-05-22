In the provided SQL code, the `WITH` clause is used to create a Common Table Expression (CTE) named `RankedPoints`. Here's a breakdown of what each part of the code is doing:

1. **Common Table Expression (CTE)**:
   ```sql
   WITH RankedPoints AS (
       SELECT 
           points,
           RANK() OVER (ORDER BY points DESC) AS position
       FROM 
           your_table_name
   )
   ```
   - This part defines a CTE called `RankedPoints`. 
   - It selects the `points` column from `your_table_name` and calculates a ranking for each row based on the `points` value in descending order using the `RANK()` window function. 
   - The result is a temporary result set that includes each `points` value along with its corresponding rank (or position).

2. **UPDATE Statement**:
   ```sql
   UPDATE your_table_name
   SET position = RankedPoints.position
   FROM RankedPoints
   WHERE your_table_name.points = RankedPoints.points;
   ```
   - This part updates the `your_table_name` table.
   - It sets the `position` column in `your_table_name` to the `position` value from the `RankedPoints` CTE.
   - The `FROM RankedPoints` clause allows the `UPDATE` statement to reference the CTE.
   - The `WHERE` clause ensures that the update only occurs for rows in `your_table_name` where the `points` value matches the `points` value in the `RankedPoints` CTE.

### Summary
Overall, this code ranks the `points` in descending order and updates the `position` column in `your_table_name` with the corresponding rank for each row based on the `points` value. The use of a CTE makes the query more organized and easier to read.