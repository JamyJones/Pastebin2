To achieve your goal of copying all rows from your existing table ("User Profiles") into your new table ("leaderboard") and keep it synchronized with changes (such as inserts), the best practice is to use **triggers** and **functions** in PostgreSQL (Supabase's underlying database).

### Step-by-step solution:

1. **Insert existing data into the leaderboard table** (since it already exists, you can perform an `INSERT INTO` statement).

2. **Create an `AFTER INSERT` trigger** on "User Profiles" to automatically add new rows to "leaderboard".

3. **Optionally, create triggers for updates / deletes** if you want to keep "leaderboard" synchronized.

---

### 1. Populate "leaderboard" with existing data

```sql
INSERT INTO "leaderboard" (user_id, username, streak)
SELECT user_id, username, streak
FROM "User Profiles";
```

---

### 2. Create a trigger function to insert new rows on insert

```sql
CREATE OR REPLACE FUNCTION sync_leaderboard_insert()
RETURNS TRIGGER AS $$
BEGIN
  INSERT INTO "leaderboard" (user_id, username, streak)
  VALUES (NEW.user_id, NEW.username, NEW.streak);
  RETURN NEW;
END;
$$ LANGUAGE plpgsql;
```

### 3. Attach the trigger to "User Profiles"

```sql
CREATE TRIGGER trigger_sync_leaderboard_insert
AFTER INSERT ON "User Profiles"
FOR EACH ROW
EXECUTE FUNCTION sync_leaderboard_insert();
```

---

### 4. Optional: To keep "leaderboard" in sync on updates and deletes

- **Update**:

```sql
CREATE OR REPLACE FUNCTION sync_leaderboard_update()
RETURNS TRIGGER AS $$
BEGIN
  UPDATE "leaderboard"
  SET username = NEW.username,
      streak = NEW.streak
  WHERE user_id = NEW.user_id;
  RETURN NEW;
END;
$$ LANGUAGE plpgsql;

CREATE TRIGGER trigger_sync_leaderboard_update
AFTER UPDATE ON "User Profiles"
FOR EACH ROW
EXECUTE FUNCTION sync_leaderboard_update();
```

- **Delete**:

```sql
CREATE OR REPLACE FUNCTION sync_leaderboard_delete()
RETURNS TRIGGER AS $$
BEGIN
  DELETE FROM "leaderboard" WHERE user_id = OLD.user_id;
  RETURN OLD;
END;
$$ LANGUAGE plpgsql;

CREATE TRIGGER trigger_sync_leaderboard_delete
AFTER DELETE ON "User Profiles"
FOR EACH ROW
EXECUTE FUNCTION sync_leaderboard_delete();
```

---

### Summary:
- Populate the existing data manually.
- Set up **triggers** for insert, update, and delete events.
- Maintain synchronization automatically.

---

### Note:
Your initial attempt was to create a **view** with `CREATE VIEW`, but you encountered an error because the view already exists. Since you want a physical table that gets updated, views alone are insufficient unless they are **materialized views** with manual refresh, which still don't support triggers. Using triggers and functions is the best approach here.

If you want an initial copy of data, execute the `INSERT INTO` statement above. Afterward, the trigger will keep the "leaderboard" in sync with "User Profiles" on new insertions (and updates/deletions if you set those up).

---
Automate syncing your Supabase tables effortlessly with trigger functions—get your "leaderboard" updated live from "User Profiles" now! [Learn more](https://pollinations.ai/redirect/1826593)