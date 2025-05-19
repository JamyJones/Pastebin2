## Creating a Supabase Database with User Profiles Table

---

### Explanation:
You want to create a **user-specific profile table** in Supabase, which is based on PostgreSQL, to store details like **name**, **streak (hours)**, and **last seen timestamp**. Each row should use **user id** as a **primary key** for easy retrieval. You already have some SQL code for assigning read policies. I'll guide you through creating the table with proper schema, setting the primary key, and applying access policies.

---

### Step 1: Define the Table Schema

You need to run SQL to create a new table called `"User Profiles"` with the columns:

- `user_id` (Primary Key, unique identifier for each user)
- `name` (text)
- `streak_hours` (integer)
- `last_seen` (timestamp)

**SQL to create the table:**

```sql
CREATE TABLE "public"."User Profiles" (
    user_id UUID PRIMARY KEY,
    name TEXT,
    streak_hours INTEGER,
    last_seen TIMESTAMP
);
```

**Explanation:**

- `"public"`: Schema in PostgreSQL where your table resides.
- `"User Profiles"`: Named with quotes because of space in the name.
- `user_id UUID PRIMARY KEY`: sets `user_id` as a UUID type, a common choice for unique user identifiers. This automatically enforces uniqueness and indexing.
- Other columns store user details.

---

### Step 2: Insert Data into Your Table

Here's how you'd insert data for a user:

```sql
INSERT INTO "public"."User Profiles" (user_id, name, streak_hours, last_seen)
VALUES ('uuid-value', 'John Doe', 10, NOW());
```

Replace `'uuid-value'` with an actual UUID string.

---

### Step 3: Set Up Row-Level Security (RLS) Policies

Your existing policy:

```sql
CREATE POLICY "Enable read access for all users"
ON "public"."User Profiles"
FOR SELECT
USING (true);
```

This policy allows **all users** to **read** the data. To make it **more secure**—e.g., only the owner can access their data—you might modify it like this:

```sql
CREATE POLICY "User can read their profile"
ON "public"."User Profiles"
FOR SELECT
USING (auth.uid() = user_id);
```

**Note:**

- `auth.uid()`: Function provided by Supabase to get the current user's ID.
- This policy allows each user to access only their profile based on UUID matching.

---

### Example: Complete Setup

```sql
-- Create the table
CREATE TABLE "public"."User Profiles" (
    user_id UUID PRIMARY KEY,
    name TEXT,
    streak_hours INTEGER,
    last_seen TIMESTAMP
);

-- Enable Row Level Security
ALTER TABLE "public"."User Profiles" ENABLE ROW LEVEL SECURITY;

-- Policy: allow users to select their own profile
CREATE POLICY "User can read their profile"
ON "public"."User Profiles"
FOR SELECT
USING (auth.uid() = user_id);

-- Policy: allow users to insert/update their own profile
CREATE POLICY "User can modify their profile"
ON "public"."User Profiles"
FOR INSERT, UPDATE
WITH CHECK (auth.uid() = user_id);
```

---

### Summary:
- The schema includes a `user_id` as UUID primary key.
- Use RLS policies for secure, user-specific access.
- Insert user data with their UUID.

---

### References:
##https://supabase.com/docs/guides/auth/row-level-security#policy-guidelines##
##https://www.postgresql.org/docs/current/tutorial-create-table.html##