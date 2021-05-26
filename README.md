# Create a project action

## Usage

This GitHub Action creates a new project in your repository. Here's an example workflow that creates a fresh sprint project every week.

```yaml
# .github/workflows/create-sprint.yml
on:
  schedule:
    - cron: 0 9 * * 1
name: Create sprint project board
jobs:
  create-project:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - run: echo "WEEK=$(date '+%B %d, %Y')" >> $GITHUB_ENV
      - uses: matthewferry/create-a-project@v1
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
        with:
          name: "Sprint: ${{ env.WEEK }}"
          description: Weekly sprint planning project
          columns: |
            📨 To do
            🧑‍💻 In progress
            ✅ Done
            🚢 Shipped
```
