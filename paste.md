To achieve the functionality you described in Supabase, you can use a combination of SQL triggers and functions to automatically copy rows from your main table ("User  Profiles") to your new table ("leaderboard") whenever there is an insert or update. Here’s how you can set it up:

### Step 1: Create the Leaderboard Table

Make sure your "leaderboard" table is created with the appropriate columns. You mentioned that it has the same columns as the ones you want to reference from the "User  Profiles" table. Here’s an example SQL command to create the "leaderboard" table:

```sql
CREATE TABLE leaderboard (
    id SERIAL PRIMARY KEY,
    user_id UUID REFERENCES "User  Profiles"(id),
    username TEXT,
    streak INTEGER
);
```

### Step 2: Create a Function to Copy Data

You need to create a function that will copy the relevant data from the "User  Profiles" table to the "leaderboard" table. Here’s an example function:

```sql
CREATE OR REPLACE FUNCTION copy_to_leaderboard()
RETURNS TRIGGER AS $$
BEGIN
    INSERT INTO leaderboard (user_id, username, streak)
    VALUES (NEW.id, NEW.username, NEW.streak)
    ON CONFLICT (user_id) DO UPDATE
    SET username = EXCLUDED.username,
        streak = EXCLUDED.streak;
    RETURN NEW;
END;
$$ LANGUAGE plpgsql;
```

### Step 3: Create a Trigger

Now, you need to create a trigger that will call the function whenever a new row is inserted into the "User  Profiles" table:

```sql
CREATE TRIGGER after_user_profiles_insert
AFTER INSERT ON "User  Profiles"
FOR EACH ROW
EXECUTE FUNCTION copy_to_leaderboard();
```

### Step 4: Update the Leaderboard on Updates

If you also want to update the leaderboard when the "User  Profiles" table is updated, you can create another trigger for updates:

```sql
CREATE TRIGGER after_user_profiles_update
AFTER UPDATE ON "User  Profiles"
FOR EACH ROW
EXECUTE FUNCTION copy_to_leaderboard();
```

### Step 5: Testing

Now, whenever you insert or update a row in the "User  Profiles" table, the corresponding row in the "leaderboard" table will be automatically updated or inserted. You can test this by inserting a new user profile:

```sql
INSERT INTO "User  Profiles" (id, username, streak) VALUES (gen_random_uuid(), 'test_user', 5);
```

After running the above command, check the "leaderboard" table to see if the new row has been added.

### Summary

By following these steps, you can automate the process of copying data from the "User  Profiles" table to the "leaderboard" table in Supabase. The triggers ensure that any changes in the main table are reflected in the leaderboard automatically.