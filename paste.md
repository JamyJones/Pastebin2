Certainly! Here is the properly formatted and cleaned version of your SQL function, following best practices for readability and consistency:

```sql
CREATE OR REPLACE FUNCTION public.sync_leaderboard_insert()
RETURNS trigger
LANGUAGE plpgsql
AS
$$
BEGIN
    -- Insert new record into the leaderboard table
    INSERT INTO leaderboard (user_id, username, streak)
    VALUES (NEW.user_id, NEW.username, NEW.streak);
    
    -- Return the new row for further processing if needed
    RETURN NEW;
END;
$$;
```

### Explanation:

- **CREATE OR REPLACE FUNCTION**: Ensures that the function is created if it doesn’t exist or replaced if it does.
- **RETURNS trigger**: Indicates that this function is intended to be used as a trigger.
- **LANGUAGE plpgsql**: Specifies the procedural language used.
- **$$ ... $$**: Delimiters for the function body, used to avoid conflicts with internal quotes.
- **BEGIN ... END;**: Block that contains the procedural code.
- **Comments**: Added for clarity.
- **Semicolon at the end of statements**: Ensures proper separation between SQL commands.

This format adheres to industry standards, making it more readable and maintainable. Remember to associate this function with an appropriate trigger to execute it upon insert or update events on the relevant table.