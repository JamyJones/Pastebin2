### Creating a Supabase Database with a User Profile Table
---  

**Explanation:**  
Supabase is built on PostgreSQL, so creating a database table follows standard SQL syntax. Here, you’ll create a "profile" table with specific columns and set the primary key to `user_id`.  

```sql
CREATE TABLE profile (
    user_id UUID PRIMARY KEY,
    name VARCHAR(255) NOT NULL,
    streak INTEGER DEFAULT 0,
    last_seen TIMESTAMP WITH TIME ZONE DEFAULT now()
);
```

- **CREATE TABLE profile:** Starts the creation of a new table named "profile".  
- **user_id UUID PRIMARY KEY:** This defines `user_id` as a unique identifier (commonly UUIDs are used for user IDs) and sets it as the primary key, ensuring each row is uniquely identified.  
- **name VARCHAR(255) NOT NULL:** Defines a `name` column as a variable-length string with maximum 255 characters, and it cannot be null.  
- **streak INTEGER DEFAULT 0:** An integer column that records hours spent; defaults to 0 if not provided.  
- **last_seen TIMESTAMP WITH TIME ZONE DEFAULT now():** Records the last activity time; defaults to the current timestamp at row creation.  

**How to execute this:**  
- Access your Supabase dashboard.  
- Go to **SQL Editor** and paste the SQL statement above.  
- Click **Run** to execute.  

---

**Practical Example:**  
Suppose you want to insert data for a user with `user_id`, name, streak, and last seen time:  

```sql
INSERT INTO profile (user_id, name, streak, last_seen) VALUES ('some-uuid', 'John Doe', 5, '2024-04-27 14:00:00+00');
```

**Retrieve Data:**  
To get data based on user ID:  

```sql
SELECT * FROM profile WHERE user_id = 'some-uuid';
```

---

**References:**  
##https://supabase.com/docs/guides/database##  
##PostgreSQL CREATE TABLE Syntax##