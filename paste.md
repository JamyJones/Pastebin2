## Retrieving a Row from Supabase Database Using JavaScript Client

---

### **Explanation**

#### **Connecting to Supabase**
To interact with Supabase using JavaScript, you first need to initialize the Supabase client. This requires your Supabase project URL and anonymous key.

```javascript
// Import the Supabase client
import { createClient } from '@supabase/supabase-js';

// Initialize Supabase
const SUPABASE_URL = 'https://YOUR_PROJECT_URL.supabase.co';
const SUPABASE_ANON_KEY = 'YOUR_ANON_KEY';
const supabase = createClient(SUPABASE_URL, SUPABASE_ANON_KEY);
```
- `createClient()` is a method from the `@supabase/supabase-js` package that initializes the connection.
- The `SUPABASE_URL` and `SUPABASE_ANON_KEY` are credentials found in your Supabase dashboard under **Settings > API**.

---

#### **Fetching a Single Row from a Table**
To retrieve a specific row from a table, use the `.select()` method along with `.eq()` to filter by a column value.

```javascript
async function getRow() {
  const { data, error } = await supabase
    .from('your_table_name')
    .select('*')
    .eq('id', 1) // Fetch row where 'id' is 1
    .single(); // Ensures only one row is returned

  if (error) {
    console.error('Error fetching row:', error);
    return;
  }

  console.log('Retrieved row:', data);
  return data;
}

getRow();
```
- `.from('your_table_name')` specifies the table to query.
- `.select('*')` retrieves all columns from the row.
- `.eq('id', 1)` filters the row where the `id` column equals `1`.
- `.single()` ensures that only one row is returned instead of an array.

---

### **Example**
If you have a table named `users` with columns `id`, `name`, and `email`, and you want to fetch the row where `id = 5`, modify the function like this:

```javascript
async function getUser() {
  const { data, error } = await supabase
    .from('users')
    .select('name, email')
    .eq('id', 5)
    .single();

  if (error) {
    console.error('Error fetching user:', error);
    return;
  }

  console.log('User details:', data);
  return data;
}

getUser();
```
This will return an object containing the `name` and `email` of the user with `id = 5`.

---

### **References**
## https://supabase.com/docs/reference/javascript/single ##
## https://onebite.dev/play-with-supabase-database-in-website-with-javascript/ ##