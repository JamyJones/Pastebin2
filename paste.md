The error `ERROR: 42830: there is no unique constraint matching given keys for referenced table "User Profiles"` occurs because PostgreSQL requires that the referenced column in the foreign key constraint has a unique constraint or primary key in the referenced table.

### How to Fix It:
Ensure that the `streak` column in the `"User Profiles"` table has either a `UNIQUE` constraint or is part of the `PRIMARY KEY`.

#### Solution:
Modify the `"User Profiles"` table to ensure `streak` is unique.

```sql
ALTER TABLE "User Profiles"
ADD CONSTRAINT user_profiles_streak_unique UNIQUE (streak);
```

Alternatively, if `streak` should be part of the primary key:

```sql
ALTER TABLE "User Profiles"
ADD PRIMARY KEY (streak);
```

Once you ensure `streak` is unique or a primary key, your foreign key constraint should work.

Let me know if you need further clarification!