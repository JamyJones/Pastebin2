The error:

```
ERROR: 42830: there is no unique constraint matching given keys for referenced table "User Profiles"
```

indicates that you are trying to create a foreign key constraint referencing a column (`streak`) in the `"User Profiles"` table, but that column does not have a unique constraint or primary key defined on it.

### Explanation:

In PostgreSQL, a foreign key must reference a column (or set of columns) that has a **unique constraint** or **primary key**. This ensures the referential integrity of the relationship.

In your case:

```sql
ALTER TABLE leaderboard
ADD CONSTRAINT streak
FOREIGN KEY (streak)
REFERENCES "User Profiles"(streak);
```

- You are attempting to create a foreign key on `leaderboard.streak` referencing `"User Profiles".streak`.
- The column `"User Profiles".streak` **must** have a unique constraint or be a primary key, but it currently is not.

### How to fix:

1. **Identify which column(s) should identify a unique profile in `"User Profiles"`.**

2. **Ensure that column(s) have a UNIQUE constraint or PRIMARY KEY.**

#### Example:

Suppose `"User Profiles"` has a primary key `user_id`. You should reference that instead:

```sql
-- Assuming 'user_id' uniquely identifies each user
ALTER TABLE leaderboard
ADD CONSTRAINT fk_user_id
FOREIGN KEY (user_id)
REFERENCES "User Profiles"(user_id);
```

---

### If you want to enforce uniqueness on `streak`, do:

```sql
ALTER TABLE "User Profiles"
ADD CONSTRAINT unique_streak
UNIQUE (streak);
```

**Note:** Make sure that the `streak` column makes sense as a referenced key and that it uniquely identifies each profile, which might not be semantically correct if multiple profiles can have the same `streak` value.

---

### Summary:

- Only columns with `PRIMARY KEY` or `UNIQUE` constraints can be referenced by a foreign key.
- To fix the error, ensure `"User Profiles".streak` has a unique constraint or change your foreign key to reference an existing unique column, like `user_id`.

---

### Practical example:

```sql
-- Add a primary key if not exists
ALTER TABLE "User Profiles"
ADD CONSTRAINT user_profiles_pk PRIMARY KEY (user_id);

-- Then create foreign key
ALTER TABLE leaderboard
ADD CONSTRAINT fk_user_id
FOREIGN KEY (user_id)
REFERENCES "User Profiles"(user_id);
```

---

Please review your `"User Profiles"` schema to determine the correct unique key to reference.