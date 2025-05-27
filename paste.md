In GitHub Actions, you can access the run ID using the built-in environment variable `GITHUB_RUN_ID`. This variable contains the unique identifier for the workflow run.

Here’s how you can use it in your GitHub Actions workflow YAML file:

```yaml
name: Example Workflow

on: [push]

jobs:
  example_job:
    runs-on: ubuntu-latest
    steps:
      - name: Print Run ID
        run: echo "The run ID is $GITHUB_RUN_ID"
```

In this example, when the workflow is triggered by a push event, it will print the run ID to the console. You can use this variable in any step where you need to reference the run ID.