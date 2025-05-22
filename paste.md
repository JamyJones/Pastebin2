To accomplish your goal of copying all rows from the "User Profiles" table into the "leaderboard" table, and ensuring that the "leaderboard" table is synchronized and automatically updated on changes to the "User Profiles" table, here is a professional approach:

---

### Step 1: **Avoid using a View if you want persistent and synchronized data**

A *view* in PostgreSQL (and Supabase) is a virtual table, and it reflects the current state of the underlying table. But based on your description, you want actual rows stored in the `leaderboard` table, not just a view.

Since the `leaderboard` table already exists, **you should perform a one-time insertion of existing data** and then set up an automation (such as a trigger) to keep it in sync.

---

### Step 2: **Copy existing data**

```sql
INSERT INTO "leaderboard" (user_id, username, streak)
SELECT user_id, username, streak
FROM "User Profiles"
ON CONFLICT (user_id) DO NOTHING; -- ignore duplicates if primary key exists
```

*Note:* Make sure that the `leaderboard` table has a primary key or unique constraint on `user_id` to prevent duplicates.

---

### Step 3: **Set up an automatic update with a trigger**

To keep the "leaderboard" synchronized with "User Profiles" on inserts and updates, create trigger functions.

---

### Step 4: **Create trigger functions**

```sql
-- Function to handle insert/update
CREATE OR REPLACE FUNCTION sync_leaderboard()
RETURNS TRIGGER AS $$
BEGIN
  -- Handle insert
  IF (TG_OP = 'INSERT') THEN
    INSERT INTO "leaderboard" (user_id, username, streak)
    VALUES (NEW.user_id, NEW.username, NEW.streak)
    ON CONFLICT (user_id) DO NOTHING;
    RETURN NEW;
  ELSIF (TG_OP = 'UPDATE') THEN
    UPDATE "leaderboard"
    SET username = NEW.username,
        streak = NEW.streak
    WHERE user_id = NEW.user_id;
    RETURN NEW;
  ELSIF (TG_OP = 'DELETE') THEN
    DELETE FROM "leaderboard"
    WHERE user_id = OLD.user_id;
    RETURN OLD;
  END IF;
  RETURN NULL; -- in case of other operations
END;
$$ LANGUAGE plpgsql;
```

---

### Step 5: **Create a trigger on the "User Profiles" table**

```sql
CREATE TRIGGER trigger_sync_leaderboard
AFTER INSERT OR UPDATE OR DELETE ON "User Profiles"
FOR EACH ROW EXECUTE FUNCTION sync_leaderboard();
```

---

### Summary

- The `INSERT INTO ... SELECT` copies existing data.
- The trigger ensures future insertions, updates, and deletions on "User Profiles" are reflected in the "leaderboard".
- This approach maintains real-time synchronization.

---

### Additional tips:

- Ensure you have appropriate primary keys and unique constraints on your tables.
- You can wrap the initial copy into a transaction for safety if needed.
- Use Supabase's SQL editor or client tools to run these SQL scripts.

Let me know if you'd like a complete script or need help with table schema adjustments!