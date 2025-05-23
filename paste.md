In PostgreSQL, data types are used to specify the nature of data stored in columns. Among numeric types, `NUMERIC` (or `DECIMAL`) is a versatile, precise data type designed for exact numeric storage, especially useful for financial and monetary calculations.

### `NUMERIC` Data Type in PostgreSQL:

- **Purpose:** Stores numbers with exact precision and scale, meaning it can hold very large or very precise decimal numbers.
- **Syntax:** `NUMERIC(precision, scale)` where:
  - `precision` (total number of digits) defaults to unlimited if not specified.
  - `scale` (number of digits after the decimal point).
- **Usage:** Suitable for calculations requiring exactness, such as currency, scientific data, or where rounding errors from floating-point types are unacceptable.

### Example:
```sql
CREATE TABLE financials (
  amount NUMERIC(15, 2) -- up to 15 digits, with 2 after decimal
);
```

### `int2`, `int4`, `int8` Data Types:
These are fixed-width integer types that store whole numbers:

| Type | Storage Size | Range of Values | Description                          |
|--------|----------------|-----------------|--------------------------------------|
| `int2` | 2 bytes        | -32,768 to +32,767 | Alias for `smallint`                |
| `int4` | 4 bytes        | -2,147,483,648 to +2,147,483,647 | Alias for `integer`        |
| `int8` | 8 bytes        | -9,223,372,036,854,775,808 to +9,223,372,036,854,775,807 | Alias for `bigint` |

### Differences:
1. **Type of Data Stored:**
   - `NUMERIC`: Stores exact decimal/numeric data, suitable for precise computations like currency.
   - `int2`, `int4`, `int8`: Store only whole numbers, no fractional part.

2. **Precision:**
   - `NUMERIC`: Can specify arbitrary precision, great for exact calculations.
   - Integer types: Fixed size, limited to their range. No fractional part, no precision beyond the whole number.

3. **Performance:**
   - Integer types are faster and more efficient for counting or indexing.
   - `NUMERIC` is more resource-intensive due to its flexibility and precision.

4. **Use Cases:**
   - Use integer types (`int2`, `int4`, `int8`) for counts, IDs, indices.
   - Use `NUMERIC` for financial data, measurements requiring exact decimal representation.

---

### Summary:
- **`NUMERIC`**: for precise decimal numbers, customizable precision and scale.
- **`int2`/`int4`/`int8`**: for fixed-range whole numbers, fixed storage width.

### Example comparisons:
```sql
-- Numeric for precise monetary value
CREATE TABLE invoice (
  total_amount NUMERIC(12, 2) -- supports exact currency figures
);

-- Integer for count
CREATE TABLE products (
  product_id INT4 PRIMARY KEY,
  quantity INT4
);
```

Understanding these differences ensures choosing the right data type for data integrity, performance, and storage efficiency in PostgreSQL.