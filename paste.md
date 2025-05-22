In Supabase, which uses PostgreSQL under the hood, copying all rows from one table to another can be efficiently achieved using an SQL `INSERT INTO ... SELECT` statement. Here's the step-by-step process:

### Assumptions:
- Both tables (`table_source` and `table_destination`) exist.
- The destination table has a compatible schema with the source table.
  
### Basic SQL Query:

```sql
INSERT INTO table_destination
SELECT * FROM table_source;
```

### Example with column selection (recommended for clarity and safety):

If the table schemas are identical, you can use:

```sql
INSERT INTO table_destination (column1, column2, column3)
SELECT column1, column2, column3 FROM table_source;
```

### Using Supabase JavaScript Client:

You can execute this SQL statement via Supabase's `rpc` or `query` method. The recommended way is to use the `sql` method with the PostgreSQL `query` execution:

```js
import { createClient } from '@supabase/supabase-js';

const supabaseUrl = 'https://your-project.supabase.co';
const supabaseKey = 'public-anonymous-key';

const supabase = createClient(supabaseUrl, supabaseKey);

async function copyTableRows() {
  const { error } = await supabase
    .rpc('execute_sql', { sql: `
      INSERT INTO table_destination (column1, column2, column3)
      SELECT column1, column2, column3 FROM table_source;
    ` });

  if (error) {
    console.error('Error copying data:', error);
  } else {
    console.log('Data copied successfully.');
  }
}
```

**Note:** Supabase does not directly support executing raw SQL via client SDK for security reasons. To execute raw SQL, you typically use the SQL editor in the Supabase dashboard or via a server environment with elevated privileges, or you set up a stored procedure or API route that executes the SQL.

### Secure and recommended approach:

- **Use SQL in the Supabase dashboard** or your backend environment with privileged access:

```sql
INSERT INTO table_destination (column1, column2, column3)
SELECT column1, column2, column3 FROM table_source;
```

- **Automate via API or Backend:** If you want to trigger the copy operation programmatically, implement an API route (e.g., in your backend server) that runs this SQL command securely.

---

### Best practices:
- Ensure data types are compatible.
- Wrap the copy in a transaction if copying large data to ensure atomicity.
- Index the destination table if needed for performance.
- Validate the data after copying.

**Summary:**
The most straightforward way is to run an `INSERT INTO ... SELECT` SQL command within your PostgreSQL environment or Supabase SQL Editor for large data sets or regular tasks. When integrating with your app, consider creating API endpoints that run such SQL commands server-side for security reasons.