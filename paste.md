Your SQL statement has a couple of issues:

1. **Referencing Table Name Format**: In SQL, table names should not be enclosed in quotes (`"User Profiles"`). If your table name contains spaces, it's best to rename it using underscores (`user_profiles`) or use backticks (`User Profiles`) if you're using MySQL.

2. **Foreign Key Reference**: Ensure that `streak` in `"User Profiles"` (or `user_profiles`) is a **primary key** or has an **unique constraint**. Foreign keys reference unique values to maintain referential integrity.

Here’s a corrected version with proper formatting:

```sql
ALTER TABLE leaderboard
ADD CONSTRAINT fk_streak
FOREIGN KEY (streak)
REFERENCES user_profiles(streak);
```

Additionally, if `streak` is **not unique**, consider structuring your relationship differently to avoid integrity issues.

Let me know if you need further clarification!