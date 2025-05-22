The SQL statement you provided attempts to add a foreign key constraint `fk_streak` to the `leaderboard` table, referencing the `streak` column in the `User Profiles` table. However, there are two issues:

1. **Table Name with Space**: In SQL, table names with spaces must be enclosed in double quotes (`"User Profiles"`) or square brackets (`[User Profiles]`) depending on the database system (PostgreSQL uses double quotes, while SQL Server supports square brackets).
2. **Missing Column**: If the `streak` column does not exist in either table, you must first create it before adding the foreign key constraint.

### Corrected SQL Statements:

#### 1. **Adding the `streak` column in `User Profiles`**:
```sql
ALTER TABLE "User Profiles"
ADD COLUMN streak INT8;
```

#### 2. **Adding the `streak` column in `leaderboard`**:
```sql
ALTER TABLE leaderboard
ADD COLUMN streak INT8;
```

#### 3. **Adding the Foreign Key Constraint Properly**:
```sql
ALTER TABLE leaderboard
ADD CONSTRAINT fk_streak
FOREIGN KEY (streak)
REFERENCES "User Profiles"(streak);
```

### Best Practices:
- Ensure that the data types match (`INT8` is a PostgreSQL alias for `BIGINT`).
- Make sure the `streak` column in `User Profiles` is the **Primary Key** or has an **Index** for performance reasons.
- If using MySQL or another database, verify its syntax for handling table names.

Would you like guidance on how to populate this column with default values?