In PostgreSQL, numeric types are used to store exact, arbitrary-precision numbers. They are ideal when you require precise decimal calculations, such as in financial applications or when you need to avoid the rounding errors associated with floating-point types.

---

### Numeric Type in PostgreSQL

- **Definition**: The `NUMERIC` (or `DECIMAL`) type stores numbers with user-defined precision and scale. You can specify the total number of digits (`precision`) and the number of digits to the right of the decimal point (`scale`).

- **Usage**:
  ```sql
  CREATE TABLE financial_records (
      amount NUMERIC(15, 2)
  );
  ```
  Here, `amount` can store numbers with up to 15 digits overall, with 2 digits after the decimal point.

- **Advantages**:
  - Arbitrary precision (can handle very large/small numbers)
  - Exact decimal representation
  - No rounding errors due to floating-point representation

- **Disadvantages**:
  - Slightly slower than fixed-size types
  - Uses more storage space depending on precision

---

### Integer Types in PostgreSQL

PostgreSQL provides fixed-size integer types, which are more efficient for storage and computation when floating-point precision isn't required:

| Type   | Storage size | Range                                       | Description                         |
|---------|--------------|----------------------------------------------|-------------------------------------|
| `smallint` | 2 bytes    | -32,768 to 32,767                            | Synonym for `int2`                 |
| `integer` or `int4` | 4 bytes | -2,147,483,648 to 2,147,483,647            | Synonym for `int4`                 |
| `bigint` or `int8` | 8 bytes | -9,223,372,036,854,775,808 to 9,223,372,036,854,775,807 | Synonym for `int8`             |

### Differences between `numeric` and integer types:

| Aspect                    | `NUMERIC`                                                    | `int2` / `int4` / `int8`                           |
|---------------------------|--------------------------------------------------------------|---------------------------------------------------|
| Precision                 | Arbitrary (user-defined)                                    | Fixed; limited by size                            |
| Storage                   | Variable (depends on precision)                               | Fixed-size (2, 4, or 8 bytes)                    |
| Usage                     | Exact decimal numbers, monetary calculations                  | Whole numbers without fractional parts           |
| Performance               | Slower due to variable-length storage                        | Faster; optimized for integer arithmetic         |
| Range                     | Depends on specified precision; effectively unlimited       | Fixed range per type                              |
| Rounding                  | No (exact representation)                                      | Not applicable                                    |

---

### Summary
- Use `NUMERIC` when you need **precise decimal representation** with **user-defined precision**, especially for financial or high-precision calculations.
- Use `int2`, `int4`, or `int8` (or their aliases) when dealing with **whole numbers** within known fixed ranges, where performance and storage efficiency are priorities.

---

### Example:

```sql
-- Numeric with specified precision and scale:
CREATE TABLE prices (
    product_id SERIAL PRIMARY KEY,
    price NUMERIC(10, 2) -- up to 8 digits before decimal, 2 after
);

-- Integer type usage:
CREATE TABLE inventory (
    item_id SERIAL PRIMARY KEY,
    quantity INT4 -- whole number, up to ~2 billion
);
```

### Additional tip:
Always choose the smallest appropriate fixed size integer type (`smallint`, `int4`, `int8`) for performance and storage reasons when fractional precision isn't needed. Use `NUMERIC` only when decimal precision is essential.