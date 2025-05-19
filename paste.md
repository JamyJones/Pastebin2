## Fetching a Row from Supabase Database Using JavaScript Client <br>
---
### **Connecting to Supabase** <br>
To interact with Supabase using JavaScript, you first need to initialize the Supabase client. This requires your **Supabase URL** and **Anon Key**, which you can find in your Supabase dashboard.

```javascript
// Import the Supabase client
import { createClient } from '@supabase/supabase-js';

// Initialize Supabase
const SUPABASE_URL = 'https://YOUR_PROJECT.supabase.co';
const SUPABASE_ANON_KEY = 'YOUR_ANON_KEY';
const supabase = createClient(SUPABASE_URL, SUPABASE_ANON_KEY);
```
---
### **Fetching a Specific Row from a Table** <br>
To retrieve a row from a table, use the `.select()` method along with a filter condition such as `.eq()` to match a specific column value.

```javascript
async function getRow(tableName, columnName, value) {
    const { data, error } = await supabase
        .from(tableName) // Specify the table name
        .select('*') // Select all columns
        .eq(columnName, value) // Filter by column value
        .single(); // Ensure only one row is returned

    if (error) {
        console.error('Error fetching row:', error);
        return null;
    }

    return data; // Return the fetched row
}
```
---
### **Breaking Down the Code** <br>
- **`.from(tableName)`** → Specifies the table to query.
- **`.select('*')`** → Retrieves all columns from the row.
- **`.eq(columnName, value)`** → Filters the row based on a column's value.
- **`.single()`** → Ensures only one row is returned (useful when expecting a unique match).
- **Error Handling** → If an error occurs, it is logged and `null` is returned.
---
### **Example Usage** <br>
```javascript
async function fetchData() {
    const row = await getRow('users', 'id', 123); // Fetch row where id = 123
    console.log('Fetched Row:', row);
}

fetchData();
```
---
### **References** <br>
## https://supabase.com/docs/reference/javascript/select ##
## https://onebite.dev/play-with-supabase-database-in-website-with-javascript/ ##