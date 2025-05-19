## Creating a Supabase Database with User-Specific Profiles and Access Policies

---

**Summary:**  
This guide explains how to set up a `profile` table in Supabase, including defining the columns and setting appropriate Row Level Security (RLS) policies so that only authenticated users can read/write their own data.

---

### Table Creation

You will define a `profile` table with columns for user-specific information, using SQL commands in the SQL editor of your Supabase project.

```sql
-- Create the profiles table
CREATE TABLE public.profiles (
    user_id uuid PRIMARY KEY,  -- Primary key linking to user, using uuid (Supabase default for auth users)
    name text,                 -- User's name
    streak integer,            -- Hours spent on the app, stored as integer
    last_seen timestamp with time zone  -- Last time the user was active
);
```

**Explanation:**  
- `user_id uuid PRIMARY KEY`  
  This defines the primary key, uniquely identifying each profile and linking it to a Supabase auth user.  
- `name text`  
  Stores the user's name.  
- `streak integer`  
  Tracks the number of hours spent, stored as an integer for simplicity.  
- `last_seen timestamp with time zone`  
  Records the last activity time, with timezone for accuracy across regions.

---

### Setting Up Policy for Authentication-Only Access

Supabase enforces RLS (Row Level Security) policies to control row access. You need to enable RLS on the `profiles` table and create policies that permit only authenticated users to read and write **their own data**.

```sql
-- Enable Row Level Security
ALTER TABLE public.profiles ENABLE ROW LEVEL SECURITY;
```

**Policy for read (SELECT):**
```sql
CREATE POLICY "Allow authenticated users to read their profile"
ON "public"."profiles"
FOR SELECT
TO authenticated -- applies to authenticated users
USING (auth.uid() = user_id);
```

**Policy for write (INSERT, UPDATE, DELETE):**
```sql
CREATE POLICY "Allow authenticated users to modify their profile"
ON "public"."profiles"
FOR ALL
TO authenticated
USING (auth.uid() = user_id)
WITH CHECK (auth.uid() = user_id);
```

**Explanation:**
- `auth.uid()` is a Supabase function that returns the UUID of the currently authenticated user.
- `USING`: condition for reading data.
- `WITH CHECK`: condition for inserting or updating data to ensure users can only modify their own record.

---

### Practical Example

Suppose a user with `user_id` = `d290f1ee-6c54-4b01-90e6-d701748f0851` logs in.  
- They can **retrieve** their profile data with:
```sql
SELECT * FROM public.profiles WHERE user_id = auth.uid();
```

- They can **update** their streak:
```sql
UPDATE public.profiles SET streak = streak + 1 WHERE user_id = auth.uid();
```

### References  
##[Supabase RLS policies](https://supabase.com/docs/guides/security/row-level-security#creating-row-level-security-policies)##  
##[Supabase CREATE TABLE Documentation](https://supabase.com/docs/reference/postgres/create-table)##  

---

**Summary:**  
You now have a complete setup to create a user-specific `profiles` table with appropriate privacy policies in Supabase. This allows each user to securely access and modify only their own data, leveraging Supabase’s authentication and RLS features.