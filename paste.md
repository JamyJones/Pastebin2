## Summary: PostgreSQL Row Level Security Policy Error and Solution

---

**Explanation:**

The error **"ERROR: 42601: WITH CHECK cannot be applied to SELECT or DELETE"** occurs because **PostgreSQL's row level security policies** apply different rules for **ALL**, **SELECT**, **INSERT**, **UPDATE**, and **DELETE** commands. In particular, **WITH CHECK** clauses are only valid for **INSERT** and **UPDATE** policies. They are **not applicable** for **SELECT** or **DELETE** policies.

---

**Detailed Breakdown:**

### What is the Error About?

- The error indicates that the **WITH CHECK** clause has been used in a **DELETE policy**.
- According to PostgreSQL documentation, **WITH CHECK** constraints **define access** for **INSERT** and **UPDATE** operations, **not** for **DELETE**.
- **DELETE policies** only require a condition without the **WITH CHECK** clause.

---

### Correct Policy Structure for DELETE

- For delete operations, only the `USING` clause is needed.
- The `USING` clause **determines which rows** a user is **allowed to delete**.
- The `WITH CHECK` clause **cannot** be used in delete policies.

### Corrected Policy Example:

```sql
CREATE POLICY "Allow authenticated users to delete their profile"
ON "public"."User Profiles"
FOR DELETE
USING ("User Id" = auth.uid());
```

- **This** policy allows **authenticated users** to delete **only their own profile** based on the condition that their **"User Id"** matches the **current user id (`auth.uid()`)**.
  
- Notice that **`WITH CHECK`** is removed because it is invalid in this context.

---

### Additional Information:

- The **`auth.uid()`** function is usually part of **PostgREST** or **auth system**; it retrieves the **current authenticated user's id**.
- Ensure your table has **appropriate access policies** enabled:

```sql
ALTER TABLE "public"."User Profiles" ENABLE ROW LEVEL SECURITY;
```

- Make sure your **policy** is correctly applied after creation:

```sql
ALTER TABLE "public"."User Profiles" ENABLE ROW LEVEL SECURITY;
```

---

## Practical Example:

Suppose a user with ID 42 wants to delete their profile. The policy:

```sql
USING ("User Id" = auth.uid());
```

**Filters the delete operation** to only affect the row where `"User Id"` is **42**.

---

## References:

## https://www.postgresql.org/docs/current/ddl-rowsecurity.html