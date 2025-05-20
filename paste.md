## Fetching a Row from Supabase Database Using JavaScript Client

---

### **Connecting to Supabase**
To interact with Supabase, you first need to initialize the client using your **Supabase URL** and **API Key**.

```javascript
// Import the Supabase client
import { createClient } from '@supabase/supabase-js';

// Initialize Supabase
const supabaseUrl = 'https://YOUR_PROJECT.supabase.co';
const supabaseKey = 'YOUR_ANON_KEY';
const supabase = createClient(supabaseUrl, supabaseKey);
```
- `createClient`: This function initializes the Supabase client.
- `supabaseUrl`: Your project's unique Supabase URL.
- `supabaseKey`: The API key required for authentication.

---

### **Fetching a Specific Row from a Table**
To retrieve a row from a table, use the `.select()` method along with a filter.

```javascript
async function getRow(tableName, columnName, value) {
    const { data, error } = await supabase
        .from(tableName)
        .select('*')
        .eq(columnName, value)
        .single(); // Ensures only one row is returned

    if (error) {
        console.error('Error fetching row:', error);
        return null;
    }

    return data;
}

// Example usage
getRow('users', 'id', 1).then(row => console.log(row));
```
- `.from(tableName)`: Specifies the table to query.
- `.select('*')`: Retrieves all columns from the row.
- `.eq(columnName, value)`: Filters the row based on a column's value.
- `.single()`: Ensures only one row is returned.

---

### **Handling Errors**
If an error occurs, it will be logged to the console. Always check for errors before using the returned data.

---

### **Example Output**
If the `users` table contains:

| id | name  | email           |
|----|-------|----------------|
| 1  | Alice | alice@email.com |

The function call `getRow('users', 'id', 1)` will return:

```json
{
    "id": 1,
    "name": "Alice",
    "email": "alice@email.com"
}
```

---

### **References**
## https://supabase.com/docs/reference/javascript/select ##
## https://onebite.dev/play-with-supabase-database-in-website-with-javascript ##

This method ensures efficient and secure retrieval of data from Supabase using JavaScript. Let me know if you need further clarification! 🚀