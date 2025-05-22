In Supabase, you can achieve this by using PostgreSQL triggers to automate the process of copying data from the `User Profiles` table to the `leaderboard` table whenever an insert, update, or delete occurs.

### Steps:
1. **Ensure Schema Consistency**: Make sure your `leaderboard` table has the same structure as `User Profiles` for the necessary columns.
2. **Create a Trigger Function**: Write a PostgreSQL function that inserts or updates the `leaderboard` table whenever changes occur in `User Profiles`.
3. **Attach the Trigger to `User Profiles`**: Create a trigger that executes your function automatically.

### Example Implementation

#### Create the Trigger Function
```sql
CREATE OR REPLACE FUNCTION update_leaderboard()
RETURNS TRIGGER AS $$
BEGIN
    -- If a new row is inserted into User Profiles, copy the data into leaderboard
    IF TG_OP = 'INSERT' THEN
        INSERT INTO leaderboard (id, name, score) -- Adjust columns accordingly
        VALUES (NEW.id, NEW.name, NEW.score);
    
    -- If a row is updated in User Profiles, update the corresponding row in leaderboard
    ELSIF TG_OP = 'UPDATE' THEN
        UPDATE leaderboard
        SET name = NEW.name, score = NEW.score
        WHERE id = NEW.id;
    
    -- If a row is deleted from User Profiles, remove it from leaderboard
    ELSIF TG_OP = 'DELETE' THEN
        DELETE FROM leaderboard WHERE id = OLD.id;
    END IF;

    RETURN NEW;
END;
$$ LANGUAGE plpgsql;
```

#### Create the Trigger
```sql
CREATE TRIGGER trigger_update_leaderboard
AFTER INSERT OR UPDATE OR DELETE ON "User Profiles"
FOR EACH ROW
EXECUTE FUNCTION update_leaderboard();
```

### Explanation:
- The function `update_leaderboard()` handles insertions, updates, and deletions.
- The trigger `trigger_update_leaderboard` ensures that the function runs automatically whenever changes occur in `User Profiles`.

#### Best Practices:
- If performance is a concern, consider indexing the foreign key columns.
- For complex syncing logic, consider background jobs instead of triggers.

This setup ensures that `leaderboard` is always up-to-date with `User Profiles`. Let me know if you need modifications based on your table structure!