Certainly! In SQL, if you want to reference a column from another table in a new one, you typically use **foreign keys** to maintain referential integrity between tables. Here's a professional SQL template demonstrating this:

```sql
-- Create the referenced table (parent table)
CREATE TABLE Users (
    user_id INT PRIMARY KEY,  -- Unique identifier for users
    username VARCHAR(100) NOT NULL
);

-- Create the new table (child table) referencing the 'user_id' column from 'Users'
CREATE TABLE Orders (
    order_id INT PRIMARY KEY,  -- Unique identifier for orders
    user_id INT,  -- Foreign key referencing 'Users'
    order_date DATE NOT NULL,
    amount DECIMAL(10, 2) NOT NULL,
    FOREIGN KEY (user_id) REFERENCES Users(user_id) ON DELETE CASCADE
);
```

### Explanation:
- The `Users` table has a `user_id` column, which serves as the **primary key**.
- The `Orders` table includes a `user_id` column that **references** the `user_id` column from `Users`, establishing a **relationship** between the two tables.
- The `FOREIGN KEY` constraint ensures data integrity by linking rows in `Orders` to existing rows in `Users`.
- The `ON DELETE CASCADE` ensures that if a user is deleted from `Users`, their associated orders in `Orders` are automatically deleted.

Would you like to add indexes or optimize queries based on this relationship?