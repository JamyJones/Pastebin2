To copy all rows from one table to another in Supabase and automate the process so that updates in the main table reflect in the new table, you can use a combination of SQL triggers and functions. Here’s how you can achieve this:

### Step 1: Create the New Table

Assuming you have already created the new table with the same column names as the main table, ensure that the structure matches.

### Step 2: Create a Function to Copy Data

You need to create a PostgreSQL function that will handle the insertion of data from the main table to the new table. Here’s an example function:

```sql
CREATE OR REPLACE FUNCTION copy_data_to_new_table()
RETURNS TRIGGER AS $$
BEGIN
    INSERT INTO new_table (column1, column2, column3)  -- Replace with your actual column names
    VALUES (NEW.column1, NEW.column2, NEW.column3);   -- Replace with your actual column names
    RETURN NEW;
END;
$$ LANGUAGE plpgsql;
```

### Step 3: Create a Trigger

Next, you need to create a trigger that will call this function whenever a new row is inserted into the main table.

```sql
CREATE TRIGGER after_insert_main_table
AFTER INSERT ON main_table  -- Replace with your actual main table name
FOR EACH ROW
EXECUTE FUNCTION copy_data_to_new_table();
```

### Step 4: Handle Updates (Optional)

If you also want to update the new table when the main table is updated, you can create another function and trigger for updates:

```sql
CREATE OR REPLACE FUNCTION update_new_table()
RETURNS TRIGGER AS $$
BEGIN
    UPDATE new_table
    SET column1 = NEW.column1, column2 = NEW.column2, column3 = NEW.column3  -- Replace with your actual column names
    WHERE id = OLD.id;  -- Assuming you have an 'id' column to match rows
    RETURN NEW;
END;
$$ LANGUAGE plpgsql;

CREATE TRIGGER after_update_main_table
AFTER UPDATE ON main_table  -- Replace with your actual main table name
FOR EACH ROW
EXECUTE FUNCTION update_new_table();
```

### Step 5: Handle Deletions (Optional)

If you want to delete corresponding rows in the new table when rows are deleted from the main table, you can create a delete trigger as well:

```sql
CREATE OR REPLACE FUNCTION delete_from_new_table()
RETURNS TRIGGER AS $$
BEGIN
    DELETE FROM new_table
    WHERE id = OLD.id;  -- Assuming you have an 'id' column to match rows
    RETURN OLD;
END;
$$ LANGUAGE plpgsql;

CREATE TRIGGER after_delete_main_table
AFTER DELETE ON main_table  -- Replace with your actual main table name
FOR EACH ROW
EXECUTE FUNCTION delete_from_new_table();
```

### Summary

1. Create a new table with the same structure as the main table.
2. Create a function to copy data from the main table to the new table.
3. Create a trigger to call this function on insertions.
4. Optionally, create additional functions and triggers for updates and deletions.

This setup will ensure that your new table is automatically updated whenever there are changes in the main table.