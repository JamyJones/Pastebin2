In Bash, you can print the current timestamp using the `date` command. If you need the timestamp in different formats, here are some common approaches:

### 1. Basic Current Timestamp:
```bash
date
```
This prints the current date and time in the default system format.

### 2. Unix Timestamp (Seconds Since Epoch):
```bash
date +%s
```
This gives the number of seconds since 1970-01-01 00:00:00 UTC.

### 3. Custom Formatted Timestamp:
```bash
date +"%Y-%m-%d %H:%M:%S"
```
This prints the timestamp in `YYYY-MM-DD HH:MM:SS` format, which is commonly used in logs.

### 4. UTC Timestamp:
```bash
date -u +"%Y-%m-%d %H:%M:%S"
```
If you need the timestamp in Coordinated Universal Time (UTC), use `-u`.

Would you like additional formatting or timezone options? Let me know if you need further refinements!