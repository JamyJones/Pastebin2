## Handling Row-Level Security (RLS) for a PostgreSQL Trigger <br>
--- <br>

### **Explanation:** <br>

**1. Overview of Row-Level Security (RLS)** <br>
Row-Level Security (RLS) in PostgreSQL ensures that users can access only specific rows within a table based on defined policies. When a table is protected by RLS, regular users may not have direct permission to insert, update, or select data unless explicitly permitted. However, functions executed with `SECURITY DEFINER` can override these restrictions, allowing access beyond the default constraints of RLS. <br>
--- <br>

**2. Security Definer in PostgreSQL** <br>
- `SECURITY DEFINER` makes a function run with the privileges of the function’s owner rather than the caller. This helps bypass RLS restrictions when necessary. 
- The `SET search_path` clause ensures the function executes within a controlled schema environment, preventing unwanted privileges from being inherited due to different schema contexts. <br>
--- <br>

**3. Implementing `SECURITY DEFINER` in the Trigger Function** <br>
To bypass RLS, modify the function definition by explicitly setting `SECURITY DEFINER`. Here is the updated function: <br>

```sql
CREATE FUNCTION public.handle_new_user()
RETURNS trigger
LANGUAGE plpgsql
SECURITY DEFINER -- Grants elevated privileges to bypass RLS
SET search_path = public -- Ensures the function executes in a controlled schema
AS $$
BEGIN
  INSERT INTO "User Profiles" (user_id, username, streak, created_on, about, profile_image_url, topics)
  VALUES (
    NEW.id,
    NEW.raw_user_meta_data ->> 'username',
    NEW.raw_user_meta_data ->> 'streak',
    NEW.created_at,
    NEW.raw_user_meta_data ->> 'about',
    NEW.raw_user_meta_data ->> 'profile_image_url',
    NEW.raw_user_meta_data ->> 'topics'
  );
  RETURN NEW;
END;
$$;
```
---
### **Example: Creating the Trigger** <br>

After defining the function, ensure the trigger activates after inserting a new row into `auth.users`: <br>

```sql
CREATE TRIGGER on_auth_user_created
  AFTER INSERT ON auth.users
  FOR EACH ROW EXECUTE FUNCTION public.handle_new_user();
```

---
### **Security Considerations** <br>
- **Owner Privileges:** Ensure that the function is owned by a user with the necessary permissions.
- **Controlled Access:** Be cautious when using `SECURITY DEFINER`—it can inadvertently introduce security vulnerabilities.
- **Restricted Usage:** Avoid granting execution privileges to unauthorized users to prevent privilege escalation.
- **Logging & Auditing:** Track function executions and changes to security settings for compliance and safety.

---
### **References** <br>
## https://www.postgresql.org/docs/current/ddl-rowsecurity.html ## <br>
## https://www.postgresql.org/docs/current/plpgsql-control-structures.html ## <br>

This setup ensures smooth execution while maintaining security compliance! 🚀 Let me know if you need additional refinements.