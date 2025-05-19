## Creating a Supabase Database and Configuring Policies for User Profiles

---

### Explanation:

**1. Creating the Table `User Profiles`:**

Supabase uses PostgreSQL as its underlying database, so SQL commands like `CREATE TABLE` are used. Your table should include:

- `user_id` — primary key, used for uniquely identifying each user.
- `name` — user's name.
- `streak_hours` — integer representing hours spent.
- `last_seen` — timestamp of last activity.

Here's how you can create this table:

```sql
CREATE TABLE "public"."User Profiles" (
    "user_id" UUID PRIMARY KEY,
    "name" VARCHAR(255),
    "streak_hours" INTEGER,
    "last_seen" TIMESTAMP
);
```

- **"public"** — schema; default in PostgreSQL.
- **UUID** — suited for unique user IDs, especially when using authentication systems like Supabase Auth.

---

**2. Creating Policies for Authentication-Restricted Access:**

Your current policy:

```sql
create policy "Enable read access for all users"
on "public"."User Profiles"
for select using (true);
```

This enables **all users**, including unauthenticated ones, to read data. To restrict access to only authenticated users, you should modify this policy:

```sql
CREATE POLICY "Allow authenticated users to read"
ON "public"."User Profiles"
FOR SELECT
USING (auth.role() = 'authenticated');
```

Similarly, for write operations:

```sql
CREATE POLICY "Allow authenticated users to insert/update"
ON "public"."User Profiles"
FOR INSERT, UPDATE
USING (auth.role() = 'authenticated');
```

- **`auth.role()`** — returns the role of the current user in Supabase; `'authenticated'` role is assigned to logged-in users.

---

**3. Setting Policy Commands:**

Ensure **Row Level Security (RLS)** is enabled on your table:

```sql
ALTER TABLE "public"."User Profiles" ENABLE ROW LEVEL SECURITY;
```

This enforces policies, restricting data access based on your rules.

---

### Example: Complete SQL for your setup

```sql
-- Enable RLS
ALTER TABLE "public"."User Profiles" ENABLE ROW LEVEL SECURITY;

-- Create the table
CREATE TABLE "public"."User Profiles" (
    "user_id" UUID PRIMARY KEY,
    "name" VARCHAR(255),
    "streak_hours" INTEGER,
    "last_seen" TIMESTAMP
);

-- Policy for read access
CREATE POLICY "Allow authenticated users to read"
ON "public"."User Profiles"
FOR SELECT
USING (auth.role() = 'authenticated');

-- Policy for write access
CREATE POLICY "Allow authenticated users to insert/update"
ON "public"."User Profiles"
FOR INSERT, UPDATE
USING (auth.role() = 'authenticated');
```

---

### Practical Summary:

- Define your user profile table with necessary columns.
- Use UUIDs for user IDs for better scalability and security.
- Enable RLS and define policies that only allow logged-in users (`auth.role() = 'authenticated'`) to read and write.
- When using Supabase, these policies enforce security, ensuring only authenticated users access their data.

---

### References:
##https://supabase.com/docs/guides/database/security
##https://www.postgresql.org/docs/current/ddl-constraints.html