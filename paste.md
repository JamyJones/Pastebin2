## updating Supabase Policy to use UserId instead of email

--- 

**Summary:**  
This guide shows how to modify a Supabase row-level security (RLS) policy to verify the user's identity using the `UserId` column (containing user IDs) instead of email, for the `public.User Profiles` table.

---

**Explanation:**

**Original Policy Purpose:**  
The existing policy verifies that the email in the JWT token matches the email in the row for update permission. It performs this for both `using` (permission check) and `with check` (validation on update).

---

**Step-by-step Modification:**

- **Identify the JWT claim:**  
  The JWT payload contains various claims. Right now, the policy extracts `'email'` with `(select auth.jwt()) ->> 'email'`.

- **Replace email verification with UserId:**  
  The primary key `UserId` (which is also the unique user ID) should be used for verification.  
  Assuming your JWT contains `'sub'` (subject), which in Supabase by default is the user's UUID, or `'UserId'`, depending on how your JWT is configured.

- **Assuming JWT contains `'sub'` claim:**  
  The default claim for user identity in Supabase is `'sub'`. It typically contains the UUID of the user.

- **Modified policy snippet:**  
  Replace all `'email'` references with `'sub'`, and compare it with `UserId` column.

---

**Modified Policy Code:**

```sql
create policy "Enable update for users based on UserId"
on "public"."User Profiles"
for update using (
  (select auth.jwt()) ->> 'sub' = UserId
)
with check (
  (select auth.jwt()) ->> 'sub' = UserId
);
```

- **Explanation of the changes:**  
  - The policy title is updated for clarity.
  - `(select auth.jwt()) ->> 'sub'` extracts the user's UUID from the JWT token.
  - The comparison checks whether this UUID matches the `UserId` column in the row, which is the primary key and should be the same as the JWT `'sub'`.

---

**Note:**  
Ensure that in your database, `UserId` is stored as text compatible with the `'sub'` claim (usually UUID strings). If `UserId` is stored differently, adjust accordingly.

---

**References:**  
##https://supabase.com/docs/guides/auth/auth-rows-and-roles##