In GitHub Actions, you can access the **run ID** of a workflow run using the built-in environment variable `GITHUB_RUN_ID`. This variable provides the unique identifier for the current workflow run.

### How to access `GITHUB_RUN_ID`

You can reference `GITHUB_RUN_ID` directly in your workflow YAML or pass it into scripts and actions.

### Example usage in a workflow

```yaml
name: Example Workflow

on:
  push:
    branches:
      - main

jobs:
  example-job:
    runs-on: ubuntu-latest
    steps:
      - name: Show run ID
        run: echo "The GitHub Actions run ID is: $GITHUB_RUN_ID"
```

### Passing the run ID into a script

If you're running a script and want to use the run ID, you can pass it as an environment variable:

```yaml
jobs:
  example-job:
    runs-on: ubuntu-latest
    steps:
      - name: Run script with run ID
        env:
          RUN_ID: $GITHUB_RUN_ID
        run: |
          echo "Run ID is: $RUN_ID"
```

### Summary

- **`GITHUB_RUN_ID`**: Unique ID for the current run.
- Available in **workflow YAML** and within **steps/scripts**.

---

**Note:** There are other related variables:
- `GITHUB_RUN_NUMBER`: Sequential number of the run.
- `GITHUB_RUN_ATTEMPT`: Number of attempts for the run.

If you'd like further details or examples, let me know!