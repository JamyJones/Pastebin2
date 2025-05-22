The error message `ERROR: 42830: there is no unique constraint matching given keys for referenced table "User Profiles"` indicates that PostgreSQL requires a unique or primary key constraint on the referenced column of the foreign key. In this case, the column `streak` in the `"User Profiles"` table does not have a unique constraint.

### Solution:
To resolve this issue, you need to ensure that the `streak` column in the `"User Profiles"` table has a `UNIQUE` constraint or is part of the `PRIMARY KEY`. Here’s how you can do it:

#### Option 1: Add a Unique Constraint
If the `streak` column should allow duplicate values but must be uniquely referenced, you can add a `UNIQUE` constraint:
```sql
ALTER TABLE "User Profiles"
ADD CONSTRAINT unique_streak UNIQUE (streak);
```

#### Option 2: Ensure It’s a Primary Key
If the `streak` column is meant to uniquely identify a row, it should be a primary key:
```sql
ALTER TABLE "User Profiles"
ADD PRIMARY KEY (streak);
```
_(Ensure that `streak` uniquely identifies rows before making it a primary key.)_

#### Option 3: Use a Different Referencing Column
If `streak` is not supposed to be unique, consider referencing a different column that has a unique constraint or primary key, such as `user_id`:
```sql
ALTER TABLE leaderboard
ADD CONSTRAINT streak FOREIGN KEY (user_id)
REFERENCES "User Profiles"(user_id);
```

### Summary:
- PostgreSQL requires foreign key references to have a `UNIQUE` constraint or `PRIMARY KEY` on the referenced column.
- Fix it by adding a `UNIQUE` constraint or making `streak` a `PRIMARY KEY`.
- If `streak` should allow duplicates, use an alternative column like `user_id`.

Let me know if you need further clarification!