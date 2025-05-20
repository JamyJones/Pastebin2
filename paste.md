To add a new column to your Supabase database table and then update a record with the new column using the JavaScript client, follow these steps:

### Step 1: Add the New Column to Your Database

First, you need to modify your database schema to include the new column. You can do this via SQL:

```sql
ALTER TABLE your_table_name ADD COLUMN new_column_name data_type;
```

For example, if you want to add a `status` column of type `text`:

```sql
ALTER TABLE your_table_name ADD COLUMN status text;
```

**Note:** Run this SQL in your Supabase SQL editor or using any database management tool.

---

### Step 2: Update the Record with the New Column

After the new column exists, you can update a specific record using the Supabase JavaScript client.

Here is example code:

```javascript
import { createClient } from '@supabase/supabase-js';

const supabaseUrl = 'https://your-project.supabase.co'
const supabaseKey = 'public-anonymous-key' // Replace with your actual API key
const supabase = createClient(supabaseUrl, supabaseKey);

async function updateRecord() {
  const { data, error } = await supabase
    .from('your_table_name')
    .update({ new_column_name: 'new_value' })  // Set your new value here
    .eq('id', 'record_id'); // Filter to select your specific record

  if (error) {
    console.error('Error updating record:', error);
  } else {
    console.log('Updated record:', data);
  }
}

updateRecord();
```

### Notes:
- Replace `'your_table_name'` with your actual table name.
- Replace `'new_column_name'` with the name of your new column.
- Replace `'new_value'` with the value you want to set.
- Replace `'record_id'` with the unique identifier of the record you want to update (e.g., primary key).

### Summary:
1. **Add the column** via SQL (`ALTER TABLE`).
2. **Update a record** with `.update()` method, setting the new column's value.

If you need further customization or have more questions, let me know!