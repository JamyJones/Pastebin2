To achieve automatic synchronization between your `User Profiles` table and your `leaderboard` table, the recommended approach is to use **PostgreSQL triggers**. Views are read-only and do not support automatic updates or insertions into other tables when data changes, unless they are **materialized views**, which still do not automatically update other tables unless refreshed manually.

### Solution overview:

1. **Insert existing data into `leaderboard`** to initialize your data.
2. **Create a trigger function** that runs on `INSERT` (and possibly `UPDATE` or `DELETE`) on `User Profiles`.
3. **Create a trigger** that invokes this function, so that when a row is added or modified in `User Profiles`, the `leaderboard` table is updated accordingly.

---

### Step 1: Populate the `leaderboard` table

Since the table already exists, you can copy the current data via:

```sql
INSERT INTO leaderboard (user_id, username, streak)
SELECT user_id, username, streak
FROM "User Profiles"
ON CONFLICT (user_id) DO UPDATE SET 
  username = EXCLUDED.username,
  streak = EXCLUDED.streak;
```

*Note*: If `leaderboard` has a primary key or unique constraint on `user_id`, you may want to handle conflicts via `ON CONFLICT`.

---

### Step 2: Create a trigger function

This function will ensure that any insert, update, or delete on the main table is reflected in the `leaderboard`.

```sql
CREATE OR REPLACE FUNCTION sync_leaderboard()
RETURNS TRIGGER AS $$
BEGIN
  IF (TG_OP = 'INSERT') THEN
    -- Insert new row into leaderboard
    INSERT INTO leaderboard (user_id, username, streak)
    VALUES (NEW.user_id, NEW.username, NEW.streak)
    ON CONFLICT (user_id) DO UPDATE SET
      username = EXCLUDED.username,
      streak = EXCLUDED.streak;
    RETURN NEW;
    
  ELSIF (TG_OP = 'UPDATE') THEN
    -- Update existing row in leaderboard
    UPDATE leaderboard
    SET username = NEW.username,
        streak = NEW.streak
    WHERE user_id = NEW.user_id;
    RETURN NEW;
    
  ELSIF (TG_OP = 'DELETE') THEN
    -- Optionally, delete from leaderboard if user profile is deleted
    DELETE FROM leaderboard WHERE user_id = OLD.user_id;
    RETURN OLD;
  END IF;
  RETURN NULL; -- should not reach here
END;
$$ LANGUAGE plpgsql;
```

---

### Step 3: Attach trigger to your main table

```sql
CREATE TRIGGER trigger_sync_leaderboard
AFTER INSERT OR UPDATE OR DELETE ON "User Profiles"
FOR EACH ROW
EXECUTE FUNCTION sync_leaderboard();
```

---

### Additional Notes:

- Ensure the `leaderboard` table has a `PRIMARY KEY` on `user_id`.
- If you want the `leaderboard` to always reflect the latest state, this approach keeps it synchronized in real-time.
- You can extend this logic to handle bulk operations additionally with a schedule or batch process if needed.

---

### Summary:

- Initialize `leaderboard` with existing data.
- Use a trigger to automate updates on data changes.
- This ensures your `leaderboard` is always up-to-date with minimal manual effort.

Would you like me to help you write the full SQL commands to execute for your specific setup?