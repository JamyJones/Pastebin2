In Supabase, you can automate copying rows from one table to another using **database triggers**. Triggers allow you to execute SQL statements whenever an event (such as an `INSERT`, `UPDATE`, or `DELETE`) occurs on a table. Given your use case, a trigger will help ensure that new records or updates in the main table are automatically reflected in the new table.

### Steps to Automate Table Synchronization:
1. **Create a Trigger Function** – This function will copy the data from the main table to the new table.
2. **Create a Trigger** – Attach the function to the main table so it runs every time a new row is inserted.

### Example SQL Implementation
#### 1. Create a Function to Copy Data
```sql
CREATE OR REPLACE FUNCTION copy_to_new_table()
RETURNS TRIGGER AS $$
BEGIN
    INSERT INTO new_table (column1, column2, column3) 
    VALUES (NEW.column1, NEW.column2, NEW.column3);
    RETURN NEW;
END;
$$ LANGUAGE plpgsql;
```

#### 2. Create a Trigger
```sql
CREATE TRIGGER sync_data
AFTER INSERT ON main_table
FOR EACH ROW
EXECUTE FUNCTION copy_to_new_table();
```
### Explanation:
- The function `copy_to_new_table()` takes the newly inserted row (`NEW`) and inserts the corresponding data into `new_table`.
- The `AFTER INSERT` trigger ensures that every new row added to `main_table` is automatically copied to `new_table`.
- If you also want updates to propagate, create another trigger with `AFTER UPDATE`.

#### Handling Updates:
If you want updates in `main_table` to reflect in `new_table`, modify your function:
```sql
CREATE OR REPLACE FUNCTION update_new_table()
RETURNS TRIGGER AS $$
BEGIN
    UPDATE new_table
    SET column1 = NEW.column1, column2 = NEW.column2, column3 = NEW.column3
    WHERE id = NEW.id;
    RETURN NEW;
END;
$$ LANGUAGE plpgsql;

CREATE TRIGGER sync_updates
AFTER UPDATE ON main_table
FOR EACH ROW
EXECUTE FUNCTION update_new_table();
```

This will ensure that changes in `main_table` are synchronized with `new_table`. Let me know if you need additional logic, such as handling deletions!