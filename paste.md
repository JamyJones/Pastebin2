Sure! You can modify your policy to check against the `UserId` column instead of `email`. Here’s the updated version:

```sql
create policy "Enable update for users based on UserId"
on "public"."User Profiles"
for update using (
  (select auth.jwt()) ->> 'sub' = UserId
) with check (
  (select auth.jwt()) ->> 'sub' = UserId
);
```

In Supabase, the `sub` (subject) field in the JWT typically holds the user's unique identifier. By replacing `email` with `UserId` and using `sub`, you ensure the policy verifies the authenticated user’s ID correctly.

Let me know if you need further adjustments!