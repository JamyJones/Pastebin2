You can achieve this automation in Supabase using PostgreSQL triggers. A trigger will allow you to automatically insert rows into the `leaderboard` table whenever a new row is inserted into the `User Profiles` table. You can also ensure that updates to the main table reflect in the `leaderboard` table.

### Steps:
1. **Ensure Both Tables Exist** – Your `User Profiles` table should already exist, and the `leaderboard` table should have columns (`user_id`, `username`, `streak`).
2. **Create a PostgreSQL Trigger** – This will automatically insert corresponding rows into `leaderboard` whenever a new row is added to `User Profiles`.

### Example Trigger:

```sql
CREATE OR REPLACE FUNCTION update_leaderboard()
RETURNS TRIGGER AS $$
BEGIN
    INSERT INTO leaderboard (user_id, username, streak)
    VALUES (NEW.user_id, NEW.username, NEW.streak);
    RETURN NEW;
END;
$$ LANGUAGE plpgsql;

CREATE TRIGGER user_profiles_insert_trigger
AFTER INSERT ON "User Profiles"
FOR EACH ROW
EXECUTE FUNCTION update_leaderboard();
```

### Explanation:
- `update_leaderboard()`: A function that automatically inserts a row into `leaderboard` when a new entry is added to `User Profiles`.
- `AFTER INSERT ON "User Profiles"`: Ensures the trigger runs after a new row is added to `User Profiles`.
- `EXECUTE FUNCTION update_leaderboard()`: Calls the function whenever a row is inserted.

### Keeping the Tables Updated:
If you want updates in `User Profiles` to reflect in `leaderboard`, you can create another trigger for `UPDATE` operations:

```sql
CREATE OR REPLACE FUNCTION sync_leaderboard()
RETURNS TRIGGER AS $$
BEGIN
    UPDATE leaderboard
    SET username = NEW.username,
        streak = NEW.streak
    WHERE user_id = NEW.user_id;
    RETURN NEW;
END;
$$ LANGUAGE plpgsql;

CREATE TRIGGER user_profiles_update_trigger
AFTER UPDATE ON "User Profiles"
FOR EACH ROW
EXECUTE FUNCTION sync_leaderboard();
```

### Summary:
- **Inserts** will copy data from `User Profiles` to `leaderboard` automatically.
- **Updates** will ensure changes in `User Profiles` are synchronized with `leaderboard`.

Using triggers in Supabase ensures that the data in your `leaderboard` table stays consistent with your `User Profiles`. Let me know if you need additional enhancements!