To print the current timestamp in Bash, you can use the `date` command with a format specifier. The most common way to get a Unix timestamp (the number of seconds since epoch 1970-01-01 00:00:00 UTC) is:

```bash
date +%s
```

**Example:**

```bash
#!/bin/bash

current_timestamp=$(date +%s)
echo "Current timestamp: $current_timestamp"
```

This will output something like:

```
Current timestamp: 1698889174
```

---

### Additional formats:

- **Formatted date/time (e.g., ISO 8601):**

```bash
date +"%Y-%m-%dT%H:%M:%S%z"
```

- **Readable date/time:**

```bash
date +"%Y-%m-%d %H:%M:%S"
```

---

### Summary:
- Use `date +%s` for Unix timestamp.
- Use `date +<format>` for custom date/time representations.

Let me know if you'd like the timestamp in a different format or with timezone considerations!