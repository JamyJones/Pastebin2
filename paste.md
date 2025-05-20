The error `syntax error at or near "UPSERT"` indicates that PostgreSQL does not support the `FOR UPSERT` clause directly in its `CREATE POLICY` syntax for Row Level Security (RLS).

### Explanation:
In PostgreSQL, RLS policies support the following actions:

- `ALL` — all operations (select, insert, update, delete)
- `SELECT`
- `INSERT`
- `UPDATE`
- `DELETE`

**There is no `UPSERT` action**. Instead, to handle "upsert" behavior (insert or update), you typically:

- Create policies for both `INSERT` and `UPDATE` as needed.
- Or, if you want the same policy to apply to multiple operations, specify `ALL`.

### Solution:
Modify your policy to use `ALL` or specifically define `INSERT` and `UPDATE` as follows:

```sql
CREATE POLICY "Give user update and insert permission"
ON storage.objects
FOR ALL -- applies to INSERT, UPDATE, DELETE, SELECT
USING (
    bucket_id = 'profile-pictures'
    AND name = auth.uid() || '/profile.jpg'
)
WITH CHECK (
    bucket_id = 'profile-pictures'
    AND name = auth.uid() || '/profile.jpg'
);
```

Or, if you want to restrict it only to insert and update:

```sql
CREATE POLICY "Give user insert and update permission"
ON storage.objects
FOR INSERT, UPDATE
USING (
    bucket_id = 'profile-pictures'
    AND name = auth.uid() || '/profile.jpg'
)
WITH CHECK (
    bucket_id = 'profile-pictures'
    AND name = auth.uid() || '/profile.jpg'
);
```

### Summary:
- **PostgreSQL's RLS policies do not support `FOR UPSERT`.**
- Use `FOR ALL` or specify `FOR INSERT, UPDATE`.
- Ensure your policies accurately reflect the intended permissions for your application logic.

### Additional:
If you want users to be able to create or update only their profile picture objects, the above policies are appropriate. If you need to allow deletion or other operations, adjust accordingly with `FOR` clause.

---

**Note:** Always test policies with `EXPLAIN` or by performing actual database operations to verify correct behavior.