In GitHub Actions, you can retrieve the **run ID** using the built-in `GITHUB_RUN_ID` environment variable. This ID is unique for each workflow run.

Here’s how you can access it in a GitHub Actions workflow:

```yaml
name: Get Run ID Example

on: [push]

jobs:
  get-run-id:
    runs-on: ubuntu-latest
    steps:
      - name: Display Run ID
        run: echo "The GitHub Actions run ID is $GITHUB_RUN_ID"
```

### Explanation:
- `$GITHUB_RUN_ID` is an environment variable provided by GitHub Actions that holds the run ID.
- The workflow prints the run ID to the console using `echo`.

If you need to use the run ID in further steps or store it in an output variable, you can do something like this:

```yaml
      - name: Save Run ID
        run: echo "RUN_ID=$GITHUB_RUN_ID" >> $GITHUB_ENV
```

This will make `RUN_ID` available to subsequent steps in the same job.

Would you like additional guidance on using this ID for logging or debugging purposes?