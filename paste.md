## Creating a Supabase Database for User Profiles

---

### Setting Up the `profiles` Table

To create a **user profile table** in Supabase, you need a table named `profiles` that contains:
- `id` (UUID, primary key, linked to the authenticated user's ID)
- `name` (TEXT, stores the user's name)
- `streak` (INTEGER, tracks hours spent)
- `last_seen` (TIMESTAMP, records last activity)

Here’s the SQL to create the table:

```sql
CREATE TABLE public.profiles (
    id UUID PRIMARY KEY REFERENCES auth.users(id) ON DELETE CASCADE,
    name TEXT NOT NULL,
    streak INTEGER DEFAULT 0,
    last_seen TIMESTAMP DEFAULT now()
);
```

This ensures that each row is uniquely identified by the user's ID and automatically deletes the profile if the user is removed.

---

### Enabling Row-Level Security (RLS)

Supabase uses **Row-Level Security (RLS)** to control access. First, enable RLS on the `profiles` table:

```sql
ALTER TABLE public.profiles ENABLE ROW LEVEL SECURITY;
```

---

### Creating Policies for Authenticated Users

To allow **only authenticated users** to read and write their own data, define policies:

#### Read Policy (Allow users to read their own profile)
```sql
CREATE POLICY "Enable read access for authenticated users"
ON public.profiles
FOR SELECT
USING (auth.uid() = id);
```

#### Write Policy (Allow users to update their own profile)
```sql
CREATE POLICY "Enable update access for authenticated users"
ON public.profiles
FOR UPDATE
USING (auth.uid() = id);
```

#### Insert Policy (Allow users to create their own profile)
```sql
CREATE POLICY "Enable insert access for authenticated users"
ON public.profiles
FOR INSERT
WITH CHECK (auth.uid() = id);
```

These policies ensure that users can only access and modify their own profile data.

---

### Example Usage in Supabase Client

To retrieve a user's profile in JavaScript:

```javascript
const { data, error } = await supabase
  .from('profiles')
  .select('*')
  .eq('id', supabase.auth.user().id);
```

To update the streak:

```javascript
const { error } = await supabase
  .from('profiles')
  .update({ streak: 5, last_seen: new Date() })
  .eq('id', supabase.auth.user().id);
```

---

### References
## https://supabase.com/docs/guides/auth/managing-user-data ##
## https://dev.to/erickson24/how-to-automatically-add-authenticated-users-to-your-supabase-database-4006 ##
## https://stackoverflow.com/questions/79385928/supabase-rls-policy-with-authenticated-users ##

This setup ensures **secure user authentication** while allowing users to manage their own profile data efficiently. 🚀 Let me know if you need further refinements!