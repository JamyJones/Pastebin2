## Reading a Row from a Supabase Database Using JavaScript Client <br>
---
To read a row from a table in Supabase using the JavaScript client, you need to use the `.select()` method provided by Supabase's API. This method allows you to fetch data from a specified table and apply filters to retrieve specific rows. <br>
---
### **Step 1: Initialize Supabase Client** <br>
Before querying the database, you need to initialize the Supabase client using your project's URL and API key. <br>

```javascript
// Import the Supabase client
import { createClient } from '@supabase/supabase-js';

// Initialize Supabase
const SUPABASE_URL = 'https://YOUR_PROJECT_URL.supabase.co';
const SUPABASE_ANON_KEY = 'YOUR_ANON_KEY';
const supabase = createClient(SUPABASE_URL, SUPABASE_ANON_KEY);
```
---
### **Step 2: Fetch a Specific Row from a Table** <br>
To retrieve a specific row, use the `.select()` method along with `.eq()` to filter by a column value. <br>

```javascript
async function getRowById(tableName, columnName, value) {
    const { data, error } = await supabase
        .from(tableName) // Specify the table name
        .select('*') // Select all columns
        .eq(columnName, value) // Filter by column value
        .single(); // Ensure only one row is returned

    if (error) {
        console.error('Error fetching row:', error);
        return null;
    }

    return data;
}

// Example usage
getRowById('users', 'id', 1).then(row => console.log(row));
```
---
### **Step 3: Explanation of Code** <br>
- **`createClient(SUPABASE_URL, SUPABASE_ANON_KEY)`**: Initializes the Supabase client using your project credentials.
- **`.from(tableName)`**: Specifies the table from which to fetch data.
- **`.select('*')`**: Retrieves all columns from the table.
- **`.eq(columnName, value)`**: Filters the query to return only rows where `columnName` matches `value`.
- **`.single()`**: Ensures that only one row is returned instead of an array.
- **`console.log(row)`**: Displays the retrieved row in the console.
---
### **Example Output** <br>
If the `users` table contains the following data:

| id | name  | email            |
|----|-------|------------------|
| 1  | Alice | alice@email.com  |
| 2  | Bob   | bob@email.com    |

Running `getRowById('users', 'id', 1)` will return:

```json
{
    "id": 1,
    "name": "Alice",
    "email": "alice@email.com"
}
```
---
### **References** <br>
## https://supabase.com/docs/reference/javascript/select ## <br>
## https://onebite.dev/play-with-supabase-database-in-website-with-javascript/ ## <br>