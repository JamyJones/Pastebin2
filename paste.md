## Creating a Supabase Database with User Profiles and Access Policies

---

### Explanation:

#### Setting up the table `profile` with user-specific details:
- To create a table called `profile` that stores user data such as `name`, `streak`, and `last_seen`, with each row linked to a user ID:
  
```sql
CREATE TABLE public.profile (
    user_id uuid PRIMARY KEY,        -- Unique identifier for each user, references the auth system’s UUID
    name text,                        -- User's name, stored as text
    streak integer,                   -- Hours spent on the site, stored as an integer
    last_seen timestamp with time zone -- Last activity timestamp, in timezone-aware format
);
```

- **Note:** The `user_id` is the primary key ensuring each user has a unique profile. It typically links to the Supabase Auth user's UUID.

#### Setting Database Policies for Authentication:
- To restrict **read** and **write** access **only** to authenticated users, you need to implement appropriate policies.

**Example Policy for SELECT (Read) access:**

```sql
create policy "Allow authenticated users to read their profile"
on "public"."profile"
for select
using (auth.uid() = user_id);
```

**Explanation:**
- `auth.uid()` fetches the current authenticated user's ID.
- The `using` clause limits rows returned to only those where the `user_id` matches the current user, ensuring each user sees only their own data.

---

**Similarly, for INSERT and UPDATE:**

```sql
create policy "Allow authenticated users to insert/update their profile"
on "public"."profile"
for all
using (auth.uid() = user_id)
with_check (auth.uid() = user_id);
```

- **`with_check`** ensures that during inserts or updates, the user can only modify their own record, linked via the `user_id`.

**Optional: Disabling access to unauthenticated users**

```sql
-- No policy will allow access unless explicitly granted, so ensure default is restrictive
```

---

### Example usage:
Suppose authenticated user with ID `uuid-1234` logs in, they can:
- insert their profile data
- update their data
- read only their profile data

This setup guarantees **security** and **privacy**, restricting visibility and modifications to the user.  

---

### References
- ##Supabase Policies Documentation##  
- ##PostgreSQL CREATE TABLE##  
- ##Using auth.uid() in Supabase policies##