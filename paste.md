You asked how the provided SQL code works and how to reference a table with a space in its name.

### Explanation of the SQL Code

```sql
ALTER TABLE leaderboard
ADD CONSTRAINT fk_streak
FOREIGN KEY (streak)
REFERENCES User Profiles(streak);
```

- `ALTER TABLE leaderboard`: Modifies the existing table named `leaderboard`.
- `ADD CONSTRAINT fk_streak`: Adds a new constraint named `fk_streak`.
- `FOREIGN KEY (streak)`: Specifies that the `streak` column in `leaderboard` will be a foreign key.
- `REFERENCES User Profiles(streak)`: The foreign key references the `streak` column in the `User Profiles` table.

### Handling Table Names with Spaces

To reference a table or column name that contains spaces, enclose the name in double quotes (standard SQL) or backticks (MySQL). For example:

#### Standard SQL (PostgreSQL, SQL Server, etc.)
```sql
ALTER TABLE leaderboard
ADD CONSTRAINT fk_streak
FOREIGN KEY (streak)
REFERENCES "User Profiles"(streak);
```

#### MySQL
```sql
ALTER TABLE leaderboard
ADD CONSTRAINT fk_streak
FOREIGN KEY (streak)
REFERENCES `User Profiles`(streak);
```

**Best Practice:**  
Avoid using spaces in table or column names to prevent quoting issues and improve maintainability.

Let me know if you need further clarification or examples!