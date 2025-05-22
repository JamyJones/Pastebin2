Let's analyze your SQL code step by step and address the issues you've raised.

---

### 1. Original SQL Code Explanation

```sql
ALTER TABLE leaderboard
ADD CONSTRAINT fk_streak
FOREIGN KEY (streak)
REFERENCES User Profiles(streak);
```

**What this code does:**
- It modifies the `leaderboard` table by adding a new constraint named `fk_streak`.
- This constraint is a **foreign key** on the `streak` column in the `leaderboard` table.
- It references the `streak` column in the `User Profiles` table (which contains a space in its name).

**However:**
- The `streak` column **must exist** in the `leaderboard` table before creating this foreign key.
- If it does **not exist**, you need to add it first.
- The same applies to the `User Profiles` table; it must have a `streak` column with a compatible data type.

---

### 2. Addressing the Space in the Table Name

SQL table names with spaces need to be delimited properly to avoid syntax errors. The correct way depends on the SQL dialect:

- **PostgreSQL, MySQL, SQL Server:** Use double quotes `"` or backticks `` ` ``.

**Examples:**

```sql
-- PostgreSQL / SQL standard
REFERENCES "User Profiles"(streak);

-- MySQL
REFERENCES `User Profiles`(streak);
```

**Best practice:**
- Always enclose such table names in double quotes or backticks to ensure proper parsing.

---

### 3. Handling the Missing `streak` Column in the `leaderboard` Table

If the `streak` column does not exist, you will need to add it before creating the foreign key constraint.

**To add a new column named `streak` of type `int8` (which is `BIGINT` in most SQL dialects):**

```sql
ALTER TABLE leaderboard
ADD COLUMN streak BIGINT;
```

---

### 4. Complete Corrected Workflow

#### Step 1: Add the new `streak` column to `leaderboard`
```sql
ALTER TABLE leaderboard
ADD COLUMN streak BIGINT;
```

#### Step 2: Ensure the `User Profiles` table has a `streak` column
```sql
ALTER TABLE "User Profiles"
ADD COLUMN streak BIGINT;
```

*(Skip this step if the `streak` column already exists)*

#### Step 3: Add the foreign key constraint with proper quoting
```sql
ALTER TABLE leaderboard
ADD CONSTRAINT fk_streak
FOREIGN KEY (streak)
REFERENCES "User Profiles"(streak);
```

---

### **Summary of best practices:**
- Enclose table names with spaces in double quotes.
- Define necessary columns before adding constraints.
- Match data types between foreign key and referenced primary/unique key.
- Use correct syntax based on your specific SQL dialect.

---

If you'd like, I can help generate a complete, ready-to-run script based on your current schema.