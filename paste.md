To copy all rows from one table to another in Supabase and automate the process of keeping the two tables in sync, you can use a combination of SQL queries and triggers. Here’s how you can achieve this:

### Step 1: Copy Existing Rows

To copy all existing rows from the `User  Profiles` table to the `leaderboard` table, you can use the following SQL query:

```sql
INSERT INTO leaderboard (column1, column2, column3)  -- replace with your actual column names
SELECT column1, column2, column3
FROM "User  Profiles";
```

Make sure to replace `column1`, `column2`, `column3`, etc., with the actual column names you want to copy.

### Step 2: Create a Trigger for Automation

To automate the process of inserting rows into the `leaderboard` table whenever a new row is added to the `User  Profiles` table, you can create a trigger. Here’s how to do it:

1. **Create a Function**: First, create a function that will handle the insertion into the `leaderboard` table.

```sql
CREATE OR REPLACE FUNCTION insert_into_leaderboard()
RETURNS TRIGGER AS $$
BEGIN
    INSERT INTO leaderboard (column1, column2, column3)  -- replace with your actual column names
    VALUES (NEW.column1, NEW.column2, NEW.column3);  -- replace with your actual column names
    RETURN NEW;
END;
$$ LANGUAGE plpgsql;
```

2. **Create a Trigger**: Next, create a trigger that calls this function whenever a new row is inserted into the `User  Profiles` table.

```sql
CREATE TRIGGER after_user_profiles_insert
AFTER INSERT ON "User  Profiles"
FOR EACH ROW
EXECUTE FUNCTION insert_into_leaderboard();
```

### Step 3: Update the Leaderboard on Row Updates

If you also want to update the `leaderboard` table when a row in the `User  Profiles` table is updated, you can modify the function and create another trigger:

1. **Modify the Function**:

```sql
CREATE OR REPLACE FUNCTION update_leaderboard()
RETURNS TRIGGER AS $$
BEGIN
    UPDATE leaderboard
    SET column1 = NEW.column1, column2 = NEW.column2, column3 = NEW.column3  -- replace with your actual column names
    WHERE id = NEW.id;  -- assuming you have an id column to match rows
    RETURN NEW;
END;
$$ LANGUAGE plpgsql;
```

2. **Create an Update Trigger**:

```sql
CREATE TRIGGER after_user_profiles_update
AFTER UPDATE ON "User  Profiles"
FOR EACH ROW
EXECUTE FUNCTION update_leaderboard();
```

### Summary

With these steps, you will have:

- Copied existing rows from `User  Profiles` to `leaderboard`.
- Set up a trigger to automatically insert new rows into `leaderboard` when new rows are added to `User  Profiles`.
- Set up another trigger to update the `leaderboard` when rows in `User  Profiles` are updated.

Make sure to test these triggers and functions in a safe environment before deploying them to production to ensure they work as expected.