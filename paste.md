To achieve this in Supabase, you can use database triggers to automatically copy and update rows in your new table whenever changes occur in the main table. Here’s how you can set it up:

### 1. **Copy all rows initially**
To populate the new table with the existing data from the main table, you can run an SQL `INSERT INTO ... SELECT` statement:

```sql
INSERT INTO new_table (column1, column2, column3)
SELECT column1, column2, column3 FROM main_table;
```

### 2. **Automate Updates Using Triggers**
Supabase, built on PostgreSQL, allows you to use triggers and functions to automatically copy data whenever changes happen.

#### Create a function for INSERT
You need to create a function that will insert data into the new table whenever a new row is added to the main table:

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

#### Create a trigger for INSERT
Attach a trigger to the main table so that the function runs automatically on every new insertion:

```sql
CREATE TRIGGER after_insert_main_table
AFTER INSERT ON main_table
FOR EACH ROW
EXECUTE FUNCTION copy_to_new_table();
```

### 3. **Automate Updates and Deletions**
If you also want updates in the main table to reflect in the new table, create another function and trigger for updates:

#### Function for UPDATE
```sql
CREATE OR REPLACE FUNCTION update_new_table()
RETURNS TRIGGER AS $$
BEGIN
  UPDATE new_table
  SET column1 = NEW.column1,
      column2 = NEW.column2,
      column3 = NEW.column3
  WHERE id = NEW.id;
  RETURN NEW;
END;
$$ LANGUAGE plpgsql;
```

#### Trigger for UPDATE
```sql
CREATE TRIGGER after_update_main_table
AFTER UPDATE ON main_table
FOR EACH ROW
EXECUTE FUNCTION update_new_table();
```

#### Handling DELETE (if required)
To ensure deletions in the main table reflect in the new table:

```sql
CREATE OR REPLACE FUNCTION delete_from_new_table()
RETURNS TRIGGER AS $$
BEGIN
  DELETE FROM new_table WHERE id = OLD.id;
  RETURN OLD;
END;
$$ LANGUAGE plpgsql;
```

```sql
CREATE TRIGGER after_delete_main_table
AFTER DELETE ON main_table
FOR EACH ROW
EXECUTE FUNCTION delete_from_new_table();
```

### Summary
- Run the initial `INSERT INTO ... SELECT` query to copy all rows.
- Use **triggers** to keep the new table updated whenever inserts, updates, or deletions occur in the main table.

This method ensures the new table mirrors the main table automatically without needing manual intervention.

Would you like any modifications to this approach, such as filtering certain columns or conditions before copying data?