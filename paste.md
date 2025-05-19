## Fetching a Row from Supabase Database Using JavaScript Client

---

### **Connecting to Supabase**
To interact with Supabase, you need to initialize the client using your project's URL and API key.

```javascript
import { createClient } from '@supabase/supabase-js';

const SUPABASE_URL = 'https://your-project.supabase.co';
const SUPABASE_ANON_KEY = 'your-anon-key';

const supabase = createClient(SUPABASE_URL, SUPABASE_ANON_KEY);
```
- `createClient()` initializes the Supabase client.
- Replace `'your-project.supabase.co'` and `'your-anon-key'` with your actual Supabase credentials.

---

### **Fetching a Specific Row**
To retrieve a row from a table, use the `.select()` method with a filter.

```javascript
async function getRow() {
    const { data, error } = await supabase
        .from('your_table_name')
        .select('*')
        .eq('id', 1) // Replace 'id' and value with your actual column and row identifier

    if (error) {
        console.error('Error fetching data:', error);
        return;
    }

    console.log('Fetched row:', data);
}

getRow();
```
- `.from('your_table_name')`: Specifies the table to query.
- `.select('*')`: Retrieves all columns.
- `.eq('id', 1)`: Filters the row where `id` equals `1`.
- `data` contains the fetched row, while `error` holds any errors encountered.

---

### **Handling Errors**
Always check for errors when querying Supabase.

```javascript
if (error) {
    console.error('Error fetching data:', error);
}
```
- This ensures that any issues (e.g., incorrect table name, missing permissions) are logged.

---

### **Example Output**
If the table contains:

| id | name  | age |
|----|-------|-----|
| 1  | Alice | 25  |

The console output will be:

```json
[
  {
    "id": 1,
    "name": "Alice",
    "age": 25
  }
]
```

---

### **References**
## https://supabase.com/docs/reference/javascript/select ##
## https://onebite.dev/play-with-supabase-database-in-website-with-javascript/ ##