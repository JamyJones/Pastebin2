You want to keep your leaderboard table in sync with your User Profiles table, automatically reflecting any inserts or updates. Here’s how you can achieve this professionally in Supabase/Postgres:

## 1. Use a View (Recommended for Read-Only Leaderboard)

If you only need to display the leaderboard and don’t need to insert/update rows directly in the leaderboard table, a view is the best solution.  
However, you’re getting the error because a table named leaderboard already exists. You cannot create a view with the same name as an existing table.

**Solution:**  
- Drop the existing leaderboard table (if it’s safe to do so), then create the view.

```sql
DROP TABLE IF EXISTS leaderboard;

CREATE VIEW leaderboard AS
SELECT user_id, username, streak
FROM "User Profiles";
```

**Best Practice:**  
- Use views for derived data that doesn’t require direct modification.

---

## 2. If You Need a Physical Table (and Automatic Sync)

If you must have a physical leaderboard table (for performance or other reasons), use triggers to keep it in sync.

### Step 1: Create the leaderboard Table

```sql
CREATE TABLE IF NOT EXISTS leaderboard (
  user_id uuid PRIMARY KEY,
  username text,
  streak integer
);
```

### Step 2: Create Triggers to Sync Data

#### Insert Trigger

```sql
CREATE OR REPLACE FUNCTION sync_leaderboard_insert()
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

CREATE TRIGGER user_profiles_insert_leaderboard
AFTER INSERT ON "User Profiles"
FOR EACH ROW EXECUTE FUNCTION sync_leaderboard_insert();
```

#### Update Trigger

```sql
CREATE OR REPLACE FUNCTION sync_leaderboard_update()
RETURNS TRIGGER AS $$
BEGIN
  UPDATE leaderboard
  SET username = NEW.username,
      streak = NEW.streak
  WHERE user_id = NEW.user_id;
  RETURN NEW;
END;
$$ LANGUAGE plpgsql;

CREATE TRIGGER user_profiles_update_leaderboard
AFTER UPDATE ON "User Profiles"
FOR EACH ROW EXECUTE FUNCTION sync_leaderboard_update();
```

#### Delete Trigger (Optional)

```sql
CREATE OR REPLACE FUNCTION sync_leaderboard_delete()
RETURNS TRIGGER AS $$
BEGIN
  DELETE FROM leaderboard WHERE user_id = OLD.user_id;
  RETURN OLD;
END;
$$ LANGUAGE plpgsql;

CREATE TRIGGER user_profiles_delete_leaderboard
AFTER DELETE ON "User Profiles"
FOR EACH ROW EXECUTE FUNCTION sync_leaderboard_delete();
```

---

## Summary

- If you only need to read from the leaderboard, use a view and drop the existing table.
- If you need a physical table, use triggers to keep it in sync with the User Profiles table.

Let me know if you need code for a specific scenario or further clarification!