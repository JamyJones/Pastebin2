## Creating a Supabase Database for User Profiles

---

### Explanation:

#### 1. Set Up Supabase Project
- First, **create a project** on [Supabase](https://supabase.com/), which provides an PostgreSQL database.
- Once created, access the **Supabase Dashboard**.

---

#### 2. Create a New Table (profiles)
- Under the **Database** tab, go to **Table Editor**.
- Click **Create Table**.
- Name the table **profiles**.

---

#### 3. Define Table Columns
- In the **columns configuration**, add necessary columns:

| Column Name | Type               | Constraints                      | Description                                         |
| -------------- | ------------------ | -------------------------------- | --------------------------------------------------- |
| id             | UUID               | PRIMARY KEY, DEFAULT gen_random_uuid() | Unique identifier for each user, primary key.  |
| name           | VARCHAR            | NOT NULL                        | User's name.                                       |
| streak_hours   | INTEGER            | DEFAULT 0                     | Hours spent on the app.                            |
| last_seen      | TIMESTAMP WITH TIME ZONE | DEFAULT now()                | Last time the user was active.                    |

- **Note:** For UUID generation, ensure the PostgreSQL extension `pgcrypto` is enabled to use `gen_random_uuid()`. Supabase typically has this enabled by default.

---

#### 4. Set Primary Key
- Set `id` as the **primary key** to uniquely identify each user profile.
- The primary key makes retrieval via user id straightforward and efficient.

---

#### 5. Insert Default or Sample Data (Optional)
- You can insert sample user data to test.

```sql
INSERT INTO profiles (id, name, streak_hours, last_seen)
VALUES
  (gen_random_uuid(), 'Alice', 5, now()),
  (gen_random_uuid(), 'Bob', 10, now());
```

---

#### 6. Access Data
- To **retrieve** profile data by user id:

```sql
SELECT * FROM profiles WHERE id = 'user-specific-uuid';
```

---

### Example:
Suppose, when a user signs up, generate a new UUID for them, and insert their profile data:

```sql
INSERT INTO profiles (id, name, streak_hours, last_seen)
VALUES (gen_random_uuid(), 'John Doe', 0, now());
```

Now, you can easily retrieve or update a user profile based on their `id`. 

---

### References:
##https://supabase.com/docs/guides/database/tables##  
##https://supabase.com/docs/reference/postgres/enabling-extensions##