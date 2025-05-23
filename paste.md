To include a `SECURITY DEFINER` clause in your trigger function to bypass Row Level Security (RLS), you need to ensure that the function is defined with the appropriate privileges. The `SECURITY DEFINER` option allows the function to execute with the privileges of the user who defined the function, rather than the user who calls it.

Here’s your modified trigger function with the `SECURITY DEFINER` clause included:

```sql
-- Inserts a row into public.profiles
CREATE FUNCTION public.handle_new_user()
RETURNS trigger
LANGUAGE plpgsql
SECURITY DEFINER
SET search_path = ''
AS $$
BEGIN
  INSERT INTO "User  Profiles" (user_id, username, streak, created_on, about, profile_image_url, topics)
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

-- Trigger the function every time a user is created
CREATE TRIGGER on_auth_user_created
  AFTER INSERT ON auth.users
  FOR EACH ROW EXECUTE PROCEDURE public.handle_new_user();
```

### Key Changes:
1. Added `SECURITY DEFINER` to the function definition to ensure it runs with the privileges of the function owner.
2. Ensured that the function and trigger definitions are properly formatted and maintain the original logic.

Make sure that the user who creates this function has the necessary permissions to insert into the `User  Profiles` table, as the function will execute with that user's privileges.