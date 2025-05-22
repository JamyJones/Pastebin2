Your SQL statement contains a couple of issues that could cause errors:

1. **Quotation Marks Around Table Name**: SQL expects table names to be referenced without quotes unless you're using a specific database system that requires quoted identifiers.
2. **Foreign Key Column Naming**: A foreign key constraint must reference an existing primary key or unique column in the `User Profiles` table. Ensure that `streak` in `User Profiles` is indexed properly.

Here's the corrected SQL version:
```sql
ALTER TABLE leaderboard
ADD CONSTRAINT fk_streak
FOREIGN KEY (streak)
REFERENCES User_Profiles(streak);
```
### Best Practices:
- Always check that the referenced column in `User Profiles` has a primary key or unique constraint.
- Use meaningful constraint names (`fk_streak` instead of just `streak`) to avoid confusion when debugging.
- Ensure both tables have matching data types for the `streak` column.

Would you like me to check if the `streak` column meets the necessary constraints before applying this change?