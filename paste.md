## Modify Supabase Policy to Check UserId Instead of Email <br>
---
### **Explanation** <br>

#### **Understanding the Existing Policy**
- The original policy checks whether the authenticated user's email (`auth.jwt() ->> 'email'`) matches the `email` column in the `User Profiles` table.
- The `auth.jwt()` function retrieves the JSON Web Token (JWT) of the currently authenticated user, allowing access to the user's claims.

#### **Modifying the Policy to Check Using `UserId`**
- Instead of checking the email, we need to ensure that the authenticated user's `UserId` matches the `UserId` column in the table.
- The `UserId` is stored as a claim in the JWT and is also the primary key of the `User Profiles` table.

#### **Updated Policy**
```sql
create policy "Enable update for users based on UserId"
on "public"."User Profiles"
for update using (
  (select auth.jwt()) ->> 'UserId' = "UserId"
) with check (
  (select auth.jwt()) ->> 'UserId' = "UserId"
);
```

#### **Breakdown of Changes**
- Replaced `(select auth.jwt()) ->> 'email' = email` with `(select auth.jwt()) ->> 'UserId' = "UserId"` to compare the `UserId`.
- This ensures that only users whose `UserId` matches the row's primary key can update that row.

---
### **Example Scenario**
Imagine a row in `User Profiles`:
```sql
UserId | Name    | Email
------ | ------ | ------------
123    | Alice  | alice@email.com
456    | Bob    | bob@email.com
```
- If Alice logs in and her JWT contains `"UserId": "123"`, she can update her profile, but **not** Bob's.
- If Bob logs in and his JWT contains `"UserId": "456"`, he can update his own profile.

---
### **References** <br>
## https://supabase.com/docs/guides/auth/jwt ##  
## https://supabase.com/docs/guides/database/policies ##  

Would you like me to refine this further or clarify any part?
