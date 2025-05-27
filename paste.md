In GitHub Actions, you can access the run ID directly via the environment variables or context objects provided by GitHub. The run ID uniquely identifies each workflow run.

### Method 1: Using the `github` context object

GitHub provides a `github` context object available within your workflows, which contains metadata about the workflow run, including the `run_id`.

```yaml
name: Example Workflow

on:
  push:
    branches:
      - main

jobs:
  example:
    runs-on: ubuntu-latest
    steps:
      - name: Get run ID
        run: echo "Run ID is ${{ github.run_id }}"
```

**Explanation:**
- `${{ github.run_id }}` dynamically pulls the current run ID during workflow execution.

### Method 2: Accessing run ID via environment variables

You can also access certain context data through environment variables, but for `run_id`, the preferred approach is the `github` context as shown above.

### Additional examples:

**Using the run ID in scripts:**

```yaml
steps:
  - name: Display Run ID
    run: |
      echo "Workflow run ID: ${{ github.run_id }}"
```

**Passing run ID as an environment variable:**

```yaml
env:
  RUN_ID: ${{ github.run_id }}

steps:
  - name: Use Run ID
    run: |
      echo "The current run ID is $RUN_ID"
```

---

### Summary:
- Use `${{ github.run_id }}` within your workflow YAML to get the run ID.
- It can be used directly in `run` commands or as part of environment variables.

Let me know if you'd like a more advanced example or integration context!