## Fetching a Row from Supabase Database Using JavaScript Client

---

### Explanation:

#### **1. Setting Up Supabase Client**
To interact with Supabase, you need to initialize the Supabase client using your project's URL and API key.

```javascript
import { createClient } from '@supabase/supabase-js';

const SUPABASE_URL = 'https://YOUR_PROJECT_URL.supabase.co';
const SUPABASE_ANON_KEY = 'YOUR_ANON_KEY';

const supabase = createClient(SUPABASE_URL, SUPABASE_ANON_KEY);
```
- `createClient` is a function from the `@supabase/supabase-js` package that initializes the Supabase client.
- `SUPABASE_URL` is the unique URL for your Supabase project.
- `SUPABASE_ANON_KEY` is the anonymous key used for authentication.

---

#### **2. Fetching a Specific Row from a Table**
To retrieve a row from a table, use the `.select()` method along with `.eq()` to filter by a specific column.

```javascript
async function getRowById(tableName, rowId) {
    const { data, error } = await supabase
        .from(tableName)
        .select('*')
        .eq('id', rowId)
        .single(); // Ensures only one row is returned

    if (error) {
        console.error('Error fetching row:', error);
        return null;
    }

    return data;
}
```
- `.from(tableName)`: Specifies the table to query.
- `.select('*')`: Fetches all columns from the row.
- `.eq('id', rowId)`: Filters the row where the `id` matches `rowId`.
- `.single()`: Ensures only one row is returned.

---

#### **3. Using the Function**
Call the function and handle the returned data.

```javascript
async function fetchData() {
    const row = await getRowById('users', 1); // Fetch row with id = 1 from 'users' table
    console.log('Fetched Row:', row);
}

fetchData();
```
- This function fetches a row from the `users` table where `id = 1` and logs the result.

---

### Example:
If your `users` table contains:

| id | name  | email           |
|----|-------|----------------|
| 1  | Alice | alice@email.com |

Calling `getRowById('users', 1)` will return:

```json
{
    "id": 1,
    "name": "Alice",
    "email": "alice@email.com"
}
```

---

### References:
## https://supabase.com/docs/reference/javascript/select ##
## https://onebite.dev/play-with-supabase-database-in-website-with-javascript/ ##