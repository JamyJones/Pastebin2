In PostgreSQL, when you have column names that contain spaces or special characters, you need to use double quotes to reference them. For example, if you want to reference the "Created at" column from the `auth.users` table, you would write your query like this:

```sql
SELECT "Created at" FROM auth.users;
```

Make sure to always use double quotes around the column name to ensure that PostgreSQL interprets it correctly. If you are using this in a more complex query, just remember to keep the double quotes around the column name wherever you reference it.