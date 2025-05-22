To copy all rows from one table to another in Supabase and automate the process of keeping the new table updated, you can use a combination of SQL queries and triggers. Here’s how you can achieve this:

### Step 1: Copy Existing Rows

To copy all existing rows from the `User  Profiles` table to the `leaderboard` table, you can use the following SQL query:

```sql
INSERT INTO leaderboard (user_id, username, streak)
SELECT user_id, username, streak
FROM "User  Profiles";
```

You can run this query in the SQL editor of Supabase to populate the `leaderboard` table with the current data from the `User  Profiles` table.

### Step 2: Create a Trigger for Automation

To ensure that the `leaderboard` table is updated automatically whenever there is an insert in the `User  Profiles` table, you can create a trigger. Here’s how to do it:

1. **Create a Function**: First, create a function that will handle the insertion into the `leaderboard` table.

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

2. **Create a Trigger**: Next, create a trigger that calls this function whenever a new row is inserted into the `User  Profiles` table.

```sql
CREATE TRIGGER insert_leaderboard
AFTER INSERT ON "User  Profiles"
FOR EACH ROW
EXECUTE FUNCTION update_leaderboard();
```

### Step 3: Test the Automation

After setting up the trigger, you can test it by inserting a new row into the `User  Profiles` table. The corresponding row should automatically be inserted into the `leaderboard` table.

### Additional Considerations

- **Updating Rows**: If you also want to update rows in the `leaderboard` table when the corresponding rows in the `User  Profiles` table are updated, you can create an additional trigger for the `UPDATE` event.
  
- **Deleting Rows**: If you want to handle deletions as well, you can create a trigger for the `DELETE` event to remove the corresponding row from the `leaderboard` table.

Here’s an example of how to create an update trigger:

```sql
CREATE OR REPLACE FUNCTION update_leaderboard_on_update()
RETURNS TRIGGER AS $$
BEGIN
    UPDATE leaderboard
    SET username = NEW.username, streak = NEW.streak
    WHERE user_id = NEW.user_id;
    RETURN NEW;
END;
$$ LANGUAGE plpgsql;

CREATE TRIGGER update_leaderboard
AFTER UPDATE ON "User  Profiles"
FOR EACH ROW
EXECUTE FUNCTION update_leaderboard_on_update();
```

And for deletion:

```sql
CREATE OR REPLACE FUNCTION delete_leaderboard()
RETURNS TRIGGER AS $$
BEGIN
    DELETE FROM leaderboard
    WHERE user_id = OLD.user_id;
    RETURN OLD;
END;
$$ LANGUAGE plpgsql;

CREATE TRIGGER delete_leaderboard
AFTER DELETE ON "User  Profiles"
FOR EACH ROW
EXECUTE FUNCTION delete_leaderboard();
```

By following these steps, you can effectively copy and automate the synchronization of data between your `User  Profiles` and `leaderboard` tables in Supabase.