Here's your SQL function formatted in a more professional and readable way, following best practices:

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

### Explanation:
1. **Consistent Formatting**: Ensured the function definition maintains a clean and structured layout for better readability.
2. **Removed Unnecessary Quotation Marks**: Unless necessary due to special characters or reserved words, it's preferable not to wrap table names in quotes.
3. **Indentation**: Each statement inside the function is properly indented for clarity.
4. **Professional Spacing**: Used consistent spacing between keywords to make the query easier to scan.

This function will be triggered whenever a relevant operation is performed on a table, inserting new rows into the `leaderboard` table. Let me know if you'd like further refinements or explanations!