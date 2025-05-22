In PostgreSQL (and thus Supabase, which uses PostgreSQL), column names that contain spaces or special characters must be quoted explicitly to be referenced correctly. The standard way is to use double quotes `" "` around the exact column name.

### Referencing a column with spaces in SQL:

Suppose the column name is `"Created at"` in the `auth.users` table.

**Example:**

```sql
SELECT id, "Created at"
FROM auth.users
WHERE "Created at" > '2023-01-01';
```

### Important points:
- Double quotes are necessary around the column name if it contains spaces or special characters.
- Always use lowercase or exact case as stored in the database, since unquoted identifiers are folded to lowercase in PostgreSQL, but quoted identifiers are case-sensitive.
- When inserting or updating, likewise, enclose column names in double quotes.

### Example insert/update:

```sql
INSERT INTO auth.users ("Created at", email)
VALUES ('2023-10-01 12:00:00', 'user@example.com');
```

### Note on Supabase:
Supabase's auto-generated `auth.users` table authenticates users but also exposes a read-only view. To reference custom columns with spaces, always quote them properly within your SQL queries or API calls.

---

**Summary:**
- Use double quotes `"` around the column names with spaces.
- Always be case-sensitive when quoting identifiers.
- Example syntax: `"Column Name with spaces"`

If you are executing this via Supabase client libraries, the same quoting rule applies within raw SQL queries.

---

**Would you like an example of a full query or a more specific use case?**

---
Master PostgreSQL quoting for spaces in columns like "Created at" with clear examples—boost your Supabase queries now! [Learn more](https://pollinations.ai/redirect/1826593)