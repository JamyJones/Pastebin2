In GitHub Actions, you can retrieve the `run_id` using the built-in `GITHUB_RUN_ID` environment variable. This unique identifier is assigned to each workflow run and can be accessed within your workflow.

### Example Usage

You can reference it in a workflow step like this:

```yaml
name: Get Run ID
on: [push]

jobs:
  get-run-id:
    runs-on: ubuntu-latest
    steps:
      - name: Display Run ID
        run: echo "Run ID: $GITHUB_RUN_ID"
```

Alternatively, if you need to use it in a script within a GitHub Actions workflow:

```bash
echo "The current workflow run ID is: $GITHUB_RUN_ID"
```

### Using `run_id` in API Calls

If you want to fetch details about a specific workflow run programmatically, you can use the GitHub API:

```bash
curl -H "Authorization: token <YOUR_GITHUB_TOKEN>" \
     -H "Accept: application/vnd.github.v3+json" \
     https://api.github.com/repos/<OWNER>/<REPO>/actions/runs/$GITHUB_RUN_ID
```

Replace `<YOUR_GITHUB_TOKEN>` with a valid personal access token and `<OWNER>/<REPO>` with the respective repository details.

Would you like guidance on handling workflow runs in other contexts?
