## Modify Supabase Policy to Check User ID <br>
---

### Explanation: <br>
In Supabase, Row-Level Security (RLS) policies use PostgreSQL functions to determine access control. The original policy checks the authenticated user's email from the JWT (`auth.jwt()`) and compares it to the email column in the `User Profiles` table. To modify this policy to check against the `UserId` column (which is the primary key), we need to extract the `user_id` from the JWT token instead.

---

### Updated Policy:<br>
Here’s how to modify the policy to check against the `UserId` column instead of the email:

```sql
create policy "Enable update for users based on UserId"
on "public"."User Profiles"
for update using (
  (select auth.jwt()) ->> 'sub' = UserId
) with check (
  (select auth.jwt()) ->> 'sub' = UserId
);
```

---

### Explanation of Changes:<br>

1. **Extracting `UserId` from JWT:**  
   - The `auth.jwt()` function retrieves the user's authentication token.  
   - The `->>` operator extracts a specific field from the JSON object.  
   - In Supabase, the authenticated user's ID is stored in the `sub` field of the JWT.  
   - Instead of checking the `'email'` field, we now extract `'sub'` (subject) to match the `UserId`.  

2. **Matching Against `UserId`:**  
   - The `UserId` column in the `User Profiles` table holds the user's unique ID.  
   - We ensure that only rows where the authenticated user's ID matches this column can be updated.  

3. **Applying `with check` Condition:**  
   - Ensures users can only update rows where their own `UserId` matches the row in the database.  
   - Prevents unauthorized changes by other users.  

---

### Example Scenario:<br>
- If a user is authenticated with Supabase and their `user_id` is `"1234"`, then:
  - The JWT contains `{ "sub": "1234" }`
  - The policy will allow updates only on rows where `UserId = '1234'`.  
  - Users cannot modify profiles that don’t match their authenticated ID.

---

### References:  
## [https://supabase.com/docs/guides/auth/auth-helpers](https://supabase.com/docs/guides/auth/auth-helpers) ##  
## [https://supabase.com/docs/guides/auth/jwt](https://supabase.com/docs/guides/auth/jwt) ##  
## [https://supabase.com/docs/guides/database/security](https://supabase.com/docs/guides/database/security) ##  
---

This ensures a proper authentication-based access control using `UserId`. 🚀 Let me know if you need more details or adjustments!
