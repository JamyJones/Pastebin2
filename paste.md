Sure! You need to modify the policy to check against the `UserId` column instead of `email`. Here's the updated version of your Supabase policy:

```sql
create policy "Enable update for users based on UserId"
on "public"."User Profiles"
for update using (
  (select auth.jwt()) ->> 'sub' = UserId
) with check (
  (select auth.jwt()) ->> 'sub' = UserId
);
```

In this version:
- The `auth.jwt()` function extracts the authenticated user's JWT payload.
- Instead of comparing the `email` field, it now checks `UserId`.
- The `sub` (subject) field inside the JWT usually represents the user's ID, which Supabase assigns during authentication.

Make sure your authentication system indeed stores the expected user ID in the JWT’s `sub` field. If Supabase uses a different field name for user IDs in the token, you might need to adjust accordingly.

Let me know if you need further tweaks!