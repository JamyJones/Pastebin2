Your SQL policy contains a few issues that need to be addressed:

### Issues:
1. **Syntax for `FOR UPSERT`**: In PostgreSQL (and specifically Supabase's Row Level Security (RLS) policies), `UPSERT` is not a valid keyword for policies. Instead, you must specify `FOR INSERT` and `FOR UPDATE` separately if you want both behaviors.
2. **Incorrect Usage of `{USING | WITH CHECK}`**: `USING` is for controlling read access, whereas `WITH CHECK` is used for restricting inserts and updates. You must use the correct one depending on your goal.
3. **Expression Mistakes**:
   - `auth.uid()::text + '/profile.jpg'`: The `+` operator does not concatenate strings in SQL. Use `||` instead.
   - `(select auth.uid()::text) = auth.user.id`: This comparison does not make sense—`auth.user.id` isn't valid in this context.

### Corrected Version:
```sql
CREATE POLICY "Give user update and insert permission"
ON storage.objects 
FOR INSERT WITH CHECK (
    bucket_id = 'profile-pictures'
    AND name = auth.uid()::text || '/profile.jpg'
);

CREATE POLICY "Give user update permission"
ON storage.objects 
FOR UPDATE USING (
    bucket_id = 'profile-pictures'
    AND name = auth.uid()::text || '/profile.jpg'
);
```
### Explanation:
- The **INSERT policy** ensures that only authenticated users can insert a profile picture with a name that follows `auth.uid() + '/profile.jpg'`.
- The **UPDATE policy** ensures that authenticated users can update objects that match their user ID.

This should work correctly in Supabase or PostgreSQL with RLS enabled. Let me know if you need further refinements.