Sure! Here's the modified policy that checks the `"UserId"` column instead of email:

```sql
create policy "Enable update for users based on UserId"
on "public"."User Profiles"
for update using (
  (select auth.jwt()) ->> 'sub' = UserId
) with check (
  (select auth.jwt()) ->> 'sub' = UserId
);
```

In Supabase, `auth.jwt()` returns the JWT of the authenticated user. Instead of `'email'`, I used `'sub'`, which typically represents the user's unique identifier (User ID) in the JWT.

Make sure that `"UserId"` in the `"public"."User Profiles"` table correctly stores the unique identifier for each authenticated user. If needed, you can verify the claims in the JWT structure via [Supabase documentation](https://supabase.com/docs).

Let me know if you need further refinements!
