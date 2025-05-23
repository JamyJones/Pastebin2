Certainly! Here is the properly formatted PostgreSQL function using standard indentation and best practices for readability:

```sql
CREATE OR REPLACE FUNCTION public.sync_leaderboard_insert()
RETURNS trigger
LANGUAGE plpgsql
AS $function$
BEGIN
    INSERT INTO leaderboard (user_id, username, streak)
    VALUES (NEW.user_id, NEW.username, NEW.streak);

    RETURN NEW;
END;
$function$;
```

**Best Practices:**
- Use consistent indentation for readability.
- Place keywords (e.g., CREATE, RETURNS, LANGUAGE) on their own lines.
- Use the same delimiter (`$function$`) at the start and end of the function body.
- Always terminate statements with a semicolon.

Let me know if you need an example of how to attach this function to a trigger or have any other questions!