## Creating a Supabase Database Table with Security Policies for User Profiles

---

### **Explanation**

#### **Table Creation:**
- To create a table called *"User Profiles"* which stores user-specific details with a primary key *"User Id"*, you will use the `CREATE TABLE` SQL statement.
- Typical columns you might want:
  - **User Id** (UUID or TEXT): Unique identifier for each user, primary key.
  - **Name** (TEXT): User's name.
  - **Streak** (INTEGER): Hours spent on a task.
  - **Last Seen** (TIMESTAMP): Last active time of the user.

**Sample SQL:**
```sql
CREATE TABLE "public"."User Profiles" (
  "User Id" UUID PRIMARY KEY,
  "Name" TEXT,
  "Streak" INTEGER,
  "Last Seen" TIMESTAMP DEFAULT now()
);
```

- **Why use UUID?** UUIDs provide a unique identifier for each user, ideal for distributed systems or when integrating with external identity providers.
- **DEFAULT now()**: automatically sets the Last Seen field on record creation.

---

#### **Security Policies for Authenticated Users:**

- Supabase uses Row Level Security (RLS) policies to control access.
- You must enable RLS and create policies allowing only authenticated users to read/write their data.

**Enabling RLS:**
```sql
ALTER TABLE "public"."User Profiles" ENABLE ROW LEVEL SECURITY;
```

---

#### **Policies:**

- **Read and Write Policy for Authenticated Users:**

```sql
-- Allow authenticated users to select their own profile
CREATE POLICY "Allow authenticated users to read their profile"
ON "public"."User Profiles"
FOR SELECT
USING ("User Id" = auth.uid());

-- Allow authenticated users to insert a new profile
CREATE POLICY "Allow authenticated users to insert profile"
ON "public"."User Profiles"
FOR INSERT
WITH CHECK ("User Id" = auth.uid());

-- Allow authenticated users to update their profile
CREATE POLICY "Allow authenticated users to update their profile"
ON "public"."User Profiles"
FOR UPDATE
WITH CHECK ("User Id" = auth.uid());

-- Similarly, for delete if needed
CREATE POLICY "Allow authenticated users to delete their profile"
ON "public"."User Profiles"
FOR DELETE
WITH CHECK ("User Id" = auth.uid());
```

- The core idea is **matching** `"User Id"` in the table with `auth.uid()`, which is a special function returning the ID of the current authenticated user.

---

### **Example: Practical Usage**
Suppose a user with ID `123e4567-e89b-12d3-a456-426614174000` logs in.  
They will only be able to read, update, or delete rows where `"User Id"` equals their own UID.  

---

### **References**
- https://supabase.com/docs/guides/auth/auth-authorization#row-level-security
- https://supabase.com/docs/guides/database/primary-keys
- https://supabase.com/docs/guides/database/policies