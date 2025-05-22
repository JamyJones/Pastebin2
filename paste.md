You want to keep your leaderboard table in sync with your User Profiles table, automatically reflecting changes (inserts/updates) in the main table. Here’s how you can achieve this professionally in Supabase/Postgres:

## 1. Use a View (Recommended for Read-Only Leaderboard)

If you only need to display the leaderboard and don’t need to insert/update rows directly in the leaderboard table, a view is the best solution.  
However, you’re getting the error because a table named leaderboard already exists. You cannot create a view with the same name as an existing table.

**Solution:**  
- Drop the existing leaderboard table (if you don’t need it as a physical table).
- Then create the view.

```sql
-- Drop the existing table if you don't need it
DROP TABLE IF EXISTS leaderboard;

-- Now create the view
CREATE VIEW leaderboard AS
SELECT user_id, username, streak
FROM "User Profiles";
```

**Best Practice:**  
- Use views for derived or computed data that doesn’t need to be written to directly.
- This approach ensures your leaderboard is always up-to-date with User Profiles.

---

## 2. If You Need a Physical Table (For Write Access or Performance)

If you must have a physical leaderboard table (for example, if you need to write to it directly or for performance reasons), you should use triggers to keep it in sync.

### Step 1: Copy Existing Data

```sql
INSERT INTO leaderboard (user_id, username, streak)
SELECT user_id, username, streak
FROM "User Profiles";
```

### Step 2: Create Triggers for Syncing

#### Insert Trigger

```sql
CREATE OR REPLACE FUNCTION sync_leaderboard_insert()
RETURNS TRIGGER AS $$
BEGIN
  INSERT INTO leaderboard (user_id, username, streak)
  VALUES (NEW.user_id, NEW.username, NEW.streak);
  RETURN NEW;
END;
$$ LANGUAGE plpgsql;

CREATE TRIGGER user_profiles_insert
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

CREATE TRIGGER user_profiles_update
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

CREATE TRIGGER user_profiles_delete
AFTER DELETE ON "User Profiles"
FOR EACH ROW EXECUTE FUNCTION sync_leaderboard_delete();
```

---

## Summary

- If you only need read access, use a view and drop the existing table.
- If you need a physical table, use triggers to keep it in sync with your main table.

Let me know if you need code for a specific scenario or further clarification!