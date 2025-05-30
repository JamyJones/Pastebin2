In Bash, you can print the current timestamp using the `date` command. The following example demonstrates how to output the current timestamp in various formats:

```bash
# Print the current timestamp in YYYY-MM-DD HH:MM:SS format
date +"%Y-%m-%d %H:%M:%S"

# Print the current timestamp as a Unix epoch time (seconds since 1970-01-01)
date +"%s"

# Print the current timestamp with nanoseconds
date +"%Y-%m-%d %H:%M:%S.%N"
```

### Explanation:
- `%Y-%m-%d %H:%M:%S` prints the timestamp in a human-readable format.
- `%s` returns the Unix timestamp, useful for time calculations.
- `%N` adds nanoseconds for higher precision.

Let me know if you need variations or integration in scripts!