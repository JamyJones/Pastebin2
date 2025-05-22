To automate the process of copying rows from your `User Profiles` table to your `leaderboard` table in Supabase, you can use a **PostgreSQL trigger**. A trigger ensures that whenever a new row is inserted or updated in `User Profiles`, the corresponding values are automatically reflected in the `leaderboard` table.

### Steps:
1. **Ensure Both Tables Exist**  
   Since you've already created both tables (`User Profiles` and `leaderboard`), verify that the columns you need (`user_id`, `username`, `streak`) exist in both tables.

2. **Create a Trigger Function**
   You need a PostgreSQL function that runs whenever a new row is inserted or updated in `User Profiles`:

   ```sql
   CREATE OR REPLACE FUNCTION update_leaderboard()
   RETURNS TRIGGER AS $$
   BEGIN
       INSERT INTO leaderboard (user_id, username, streak)
       VALUES (NEW.user_id, NEW.username, NEW.streak)
       ON CONFLICT (user_id) 
       DO UPDATE SET username = EXCLUDED.username, streak = EXCLUDED.streak;
       RETURN NEW;
   END;
   $$ LANGUAGE plpgsql;
   ```

   - This function inserts the new row into `leaderboard` and updates existing records if a `user_id` already exists.

3. **Create the Trigger**
   Attach this function to the `User Profiles` table so that it automatically runs whenever an insert or update occurs:

   ```sql
   CREATE TRIGGER user_profiles_trigger
   AFTER INSERT OR UPDATE ON "User Profiles"
   FOR EACH ROW
   EXECUTE FUNCTION update_leaderboard();
   ```

### Explanation:
- The **trigger function** ensures that every time a new entry is added or updated in `User Profiles`, the corresponding row in `leaderboard` is updated.
- The `ON CONFLICT` clause ensures updates occur if the `user_id` already exists.

### Alternative Approach:
If you want to pull data dynamically instead of storing it separately, you can use a **VIEW**:

```sql
CREATE VIEW leaderboard AS
SELECT user_id, username, streak
FROM "User Profiles";
```

This ensures `leaderboard` always reflects `User Profiles` **without needing a trigger**.

Let me know if you need modifications! 🚀