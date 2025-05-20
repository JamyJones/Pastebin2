The error you're encountering:

```
ERROR: 42601: syntax error at or near "UPSERT"
LINE 3: FOR UPSERT
            ^
```

indicates that the `FOR UPSERT` clause in your policy definition is invalid in PostgreSQL, which is what Supabase uses under the hood.

### Correct Policy Syntax

PostgreSQL policy syntax supports the following `FOR` options:

- `ALL` — for all operations (SELECT, INSERT, UPDATE, DELETE)
- `SELECT` — for SELECT statements
- `INSERT` — for inserts
- `UPDATE` — for updates
- `DELETE` — for delete statements

**Note:** There is no `UPSERT` operation explicitly; `UPSERT` (or `INSERT ... ON CONFLICT`) combines insert and update but in policies, you only specify `INSERT`, `UPDATE`, etc.

### Solution

If your intent is to allow both insertions and updates — i.e., upsert behavior — you need to set policies for both `INSERT` and `UPDATE`. 

Here's what your policy should look like:

```sql
CREATE POLICY "Give user update and insert permission"
ON storage.objects
FOR ALL  -- covers INSERT, UPDATE, DELETE, and SELECT if needed
USING (
    bucket_id = 'profile-pictures'
    AND name = auth.uid() || '/profile.jpg'
)
WITH CHECK (
    bucket_id = 'profile-pictures'
    AND name = auth.uid() || '/profile.jpg'
);
```

Or, if you want to be more specific, for insert and update separately:

```sql
CREATE POLICY "Allow user to insert profile picture"
ON storage.objects
FOR INSERT
WITH CHECK (
    bucket_id = 'profile-pictures'
    AND name = auth.uid() || '/profile.jpg'
);

CREATE POLICY "Allow user to update profile picture"
ON storage.objects
FOR UPDATE
USING (
    bucket_id = 'profile-pictures'
    AND name = auth.uid() || '/profile.jpg'
);
```

### Summary

- Replace `FOR UPSERT` with `FOR ALL` or `FOR INSERT` and `FOR UPDATE` as needed.
- Confirm that your policies exactly match your intended access control.

Let me know if you'd like further assistance on policy configurations or best practices for securing your storage!