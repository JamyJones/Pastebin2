To achieve your goal of copying all rows from the "User  Profiles" table to the "leaderboard" table and keeping the "leaderboard" table updated automatically, you can use a combination of triggers and functions in Supabase (which is built on PostgreSQL).

### Step 1: Copy Existing Rows

First, you need to copy the existing rows from the "User  Profiles" table to the "leaderboard" table. You can do this with an `INSERT INTO ... SELECT` statement:

```sql
INSERT INTO leaderboard (user_id, username, streak)
SELECT user_id, username, streak
FROM "User  Profiles";
```

### Step 2: Create a Trigger Function

Next, you need to create a trigger function that will automatically insert a new row into the "leaderboard" table whenever a new row is inserted into the "User  Profiles" table.

```sql
CREATE OR REPLACE FUNCTION update_leaderboard()
RETURNS TRIGGER AS $$
BEGIN
    INSERT INTO leaderboard (user_id, username, streak)
    VALUES (NEW.user_id, NEW.username, NEW.streak);
    RETURN NEW;
END;
$$ LANGUAGE plpgsql;
```

### Step 3: Create a Trigger

Now, you need to create a trigger that will call the function you just created whenever a new row is inserted into the "User  Profiles" table.

```sql
CREATE TRIGGER insert_leaderboard
AFTER INSERT ON "User  Profiles"
FOR EACH ROW
EXECUTE FUNCTION update_leaderboard();
```

### Step 4: Update on Row Changes (Optional)

If you also want to update the "leaderboard" table when existing rows in the "User  Profiles" table are updated, you can create another trigger function and trigger for updates:

#### Update Function

```sql
CREATE OR REPLACE FUNCTION update_leaderboard_on_update()
RETURNS TRIGGER AS $$
BEGIN
    UPDATE leaderboard
    SET username = NEW.username,
        streak = NEW.streak
    WHERE user_id = NEW.user_id;
    RETURN NEW;
END;
$$ LANGUAGE plpgsql;
```

#### Update Trigger

```sql
CREATE TRIGGER update_leaderboard
AFTER UPDATE ON "User  Profiles"
FOR EACH ROW
EXECUTE FUNCTION update_leaderboard_on_update();
```

### Summary

1. Use the `INSERT INTO ... SELECT` statement to copy existing rows.
2. Create a trigger function to insert new rows into the "leaderboard" table when new rows are added to the "User  Profiles" table.
3. Optionally, create another trigger function and trigger to update the "leaderboard" table when rows in the "User  Profiles" table are updated.

This setup will ensure that your "leaderboard" table is automatically populated and updated based on changes in the "User  Profiles" table.