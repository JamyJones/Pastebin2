## Summary
Adding `SECURITY DEFINER` to a PostgreSQL trigger function to bypass Row Level Security (RLS)

---

### Explanation:

**1. What is a `SECURITY DEFINER`?**  
- It’s an option used in PostgreSQL to execute a function with the privileges of the user who defined it (the owner), rather than the privileges of the user calling it.  
- This is useful when you want certain operations inside the function to bypass RLS policies that restrict access based on the current user's privileges.

**2. How to add `SECURITY DEFINER` to your existing trigger function?**  
- You need to alter the function to specify `SECURITY DEFINER`.  
- In your provided code, the function is already declared with `language plpgsql security definer`, but your syntax is incorrect.

**3. Correct Syntax for adding `SECURITY DEFINER`**  
- The proper way to declare a function with `SECURITY DEFINER` in PostgreSQL is like this:  
```sql
CREATE FUNCTION function_name(...) RETURNS ... LANGUAGE plpgsql SECURITY DEFINER AS $$ ... $$
```
- **Note**: `SECURITY DEFINER` should come right after the language specification, not after `set search_path = ''`.

**4. Modifying your code**  
- Incorporate `SECURITY DEFINER` correctly in your function declaration.

---

### Corrected Version of Your Function:

```sql
CREATE OR REPLACE FUNCTION public.handle_new_user()
RETURNS trigger
LANGUAGE plpgsql
SECURITY DEFINER  -- Ensure this is placed correctly after the language spec
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

### Additional Notes:
- Make sure the **user who creates this function** has the privilege to **CREATE FUNCTION** with `SECURITY DEFINER`.
- The **owner of this function** will determine its privilege level; typically, `postgres` or a designated admin user.
- You may need to **set the ownership** explicitly:

```sql
ALTER FUNCTION public.handle_new_user() OWNER TO your_admin_user;
```

### Lastly:
- The trigger creation remains the same.
```sql
CREATE TRIGGER on_auth_user_created
AFTER INSERT ON auth.users
FOR EACH ROW EXECUTE PROCEDURE public.handle_new_user();
```

---

### Example:
**Scenario:**  
Suppose your RLS policies restrict access to `"User Profiles"` based on the `user_id`. Using a `SECURITY DEFINER` function allows the insert operation to bypass these restrictions, provided the owner of the function has the necessary privileges.

---

### References:
##https://www.postgresql.org/docs/current/privileges-set-user.html##  
##https://www.postgresql.org/docs/current/plpga.html##