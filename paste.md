To achieve automatic updates in your `leaderboard` table whenever changes occur in your `User Profiles` table in Supabase, you need to use triggers. Triggers are database mechanisms that run predefined actions when a certain event happens, such as `INSERT`, `UPDATE`, or `DELETE`.

### Steps to Automate Data Copying:
1. **Use a `TRIGGER` with a `FUNCTION`** to insert data into `leaderboard` whenever a new row is inserted in `User Profiles`.
2. **Ensure updates in `User Profiles` reflect in `leaderboard`**.
3. **Optional: Handle deletions if needed**.

### SQL Implementation:
#### 1. Create the Function:
You need a PostgreSQL function that inserts data into `leaderboard` when a new row is inserted into `User Profiles`.

```sql
CREATE OR REPLACE FUNCTION update_leaderboard()
RETURNS TRIGGER AS $$
BEGIN
  INSERT INTO leaderboard (user_id, username, streak)
  VALUES (NEW.user_id, NEW.username, NEW.streak)
  ON CONFLICT (user_id) DO UPDATE 
  SET username = EXCLUDED.username, 
      streak = EXCLUDED.streak;
  RETURN NEW;
END;
$$ LANGUAGE plpgsql;
```
This function ensures:
- When a new row is inserted, the corresponding row is added to `leaderboard`.
- If a row already exists (same `user_id`), it updates the existing entry.

#### 2. Create the Trigger:
Now, attach this function to your `User Profiles` table so that it runs automatically on `INSERT` events.

```sql
CREATE TRIGGER user_profiles_trigger
AFTER INSERT OR UPDATE ON "User Profiles"
FOR EACH ROW
EXECUTE FUNCTION update_leaderboard();
```

### Explanation:
- `AFTER INSERT OR UPDATE` ensures this runs when a new row is added or updated.
- `NEW` represents the new row being inserted or updated.
- `ON CONFLICT (user_id)` makes sure duplicate entries are updated instead of causing errors.

### Considerations:
- If you want to delete users from `leaderboard` when they are deleted from `User Profiles`, you can create another trigger for `DELETE`.
- Ensure your `leaderboard` table has a `PRIMARY KEY` on `user_id` for proper conflict handling.

This setup will make sure your `leaderboard` table stays synchronized with `User Profiles` automatically. Let me know if you need modifications based on specific requirements!