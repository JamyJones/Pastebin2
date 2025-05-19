## Creating a Supabase Database for User Profiles

---

### Explanation

#### **1. Setting Up the User Profile Table**
To create a `profiles` table that stores user details, including `name`, `streak`, and `last_seen`, while ensuring each row is uniquely identified by the user's ID, you can use the following SQL:

```sql
CREATE TABLE public.profiles (
    id UUID PRIMARY KEY REFERENCES auth.users(id) ON DELETE CASCADE,
    name TEXT NOT NULL,
    streak INT DEFAULT 0,
    last_seen TIMESTAMP DEFAULT now()
);
```

- **`id UUID PRIMARY KEY REFERENCES auth.users(id) ON DELETE CASCADE`**: Ensures that each profile is linked to a user in the `auth.users` table and deletes the profile if the user is removed.
- **`name TEXT NOT NULL`**: Stores the user's name.
- **`streak INT DEFAULT 0`**: Tracks the number of hours spent on the site.
- **`last_seen TIMESTAMP DEFAULT now()`**: Records the last time the user was active.

---

#### **2. Enabling Row-Level Security (RLS)**
Supabase requires **Row-Level Security (RLS)** to be enabled for policies to take effect:

```sql
ALTER TABLE public.profiles ENABLE ROW LEVEL SECURITY;
```

This ensures that unauthorized users cannot access the table.

---

#### **3. Creating Policies for Authenticated Users**
To allow only authenticated users to read and write their own data, you need to define policies:

##### **Read Policy (Allow users to read their own data)**
```sql
CREATE POLICY "Enable read access for authenticated users"
ON public.profiles
FOR SELECT
USING (auth.uid() = id);
```

##### **Write Policy (Allow users to update their own data)**
```sql
CREATE POLICY "Enable write access for authenticated users"
ON public.profiles
FOR UPDATE
USING (auth.uid() = id);
```

- **`auth.uid()`**: Retrieves the currently authenticated user's ID.
- **`USING (auth.uid() = id)`**: Ensures users can only access their own data.

---

### Example Usage in Supabase API

To retrieve a user's profile in JavaScript:

```javascript
const { data, error } = await supabase
  .from('profiles')
  .select('*')
  .eq('id', supabase.auth.user().id);

console.log(data);
```

This fetches the profile of the currently authenticated user.

---

### References
## https://supabase.com/docs/guides/auth/managing-user-data ##
## https://stackoverflow.com/questions/78550922/how-do-i-authorise-users-with-username-in-supabase ##
## https://github.com/orgs/supabase/discussions/3491 ##

Would you like additional customization for your database setup? 🚀