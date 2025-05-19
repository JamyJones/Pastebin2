## Summary
Understanding the error related to PostgreSQL row-level security policies, specifically the misuse of `WITH CHECK` in delete operations.

---

### Explanation

**ERROR: 42601: WITH CHECK cannot be applied to SELECT or DELETE**

This error occurs because PostgreSQL's **row-level security policies** are implemented differently for **SELECT**, **UPDATE**, and **DELETE** operations.

- **`WITH CHECK`**: Defines the condition for **inserting** or **updating** rows in a table.
- **`USING`**: Defines the condition for **selecting** or **deleting** rows.

In other words, for **DELETE** operations, only the `USING` clause can be used to specify who can delete a particular row. The `WITH CHECK` clause is **not applicable** to `DELETE` statements, which is why PostgreSQL throws this error.

---

### Why the Error Occurs in Your Script

Your policy:

```sql
CREATE POLICY "Allow authenticated users to delete their profile"
ON "public"."User Profiles"
FOR DELETE
WITH CHECK ("User Id" = auth.uid());
```

- **Incorrect Usage**: You are trying to apply `WITH CHECK` for a `DELETE` operation, which is **not valid** in PostgreSQL.

### How to Correct It

- Use the `USING` clause for `DELETE` policies instead of `WITH CHECK`.
  
**Corrected version:**

```sql
CREATE POLICY "Allow authenticated users to delete their profile"
ON "public"."User Profiles"
FOR DELETE
USING ("User Id" = auth.uid());
```

**Explanation of Changes:**

- Replaces `WITH CHECK` with `USING`.
- Ensures only the owner (`"User Id" = auth.uid()`) can delete their profile.
- This is the **correct approach** for `DELETE` policies.

---

### Practical Example

Suppose:

- There is a table `"public"."User Profiles"` with columns: `"User Id"` and others.
- A user is authenticated, and `auth.uid()` fetches the current user's ID.
- Only the owner should be able to delete their profile.

**Correct policy:**

```sql
CREATE POLICY "Allow users to delete their profile"
ON "public"."User Profiles"
FOR DELETE
USING ("User Id" = auth.uid());
```

This policy applies when a delete action is attempted, granting permission **only if** the `"User Id"` matches the current authenticated user.

---

### References

##https://www.postgresql.org/docs/current/ddl-rowsecurity.html