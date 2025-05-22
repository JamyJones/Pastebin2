In Supabase, you can copy all rows from one table to another using SQL `INSERT INTO ... SELECT` statements. Here’s a simple way to do it:

```sql
INSERT INTO target_table
SELECT * FROM source_table;
```

This will copy all rows from `source_table` to `target_table`. However, you need to ensure that both tables have the same schema (column structure). If they don’t, you should specify the columns explicitly:

```sql
INSERT INTO target_table (column1, column2, column3)
SELECT column1, column2, column3 FROM source_table;
```

### Handling Unique Constraints:
- If the `target_table` has unique constraints (like a primary key), ensure that the data being copied does not violate them.
- If necessary, use `ON CONFLICT` handling:

```sql
INSERT INTO target_table (column1, column2, column3)
SELECT column1, column2, column3 FROM source_table
ON CONFLICT (primary_key_column) DO NOTHING;
```

### Copying Data via Supabase Functions:
Alternatively, if you are working in a Supabase function, you can use the Supabase client library (`@supabase/supabase-js` in JavaScript) to do the same using:

```javascript
const { data, error } = await supabase
  .from('target_table')
  .insert(
    await supabase.from('source_table').select('*')
  );

if (error) console.error(error);
else console.log('Rows copied successfully:', data);
```

Let me know if you need a tailored approach based on your exact schema setup.