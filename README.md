# issue-finder
A high-performance GitHub Action designed to aggregate issues across multiple repositories based on a list of defined labels. This tool generates a centralized dashboard within the GitHub Actions Summary UI, facilitating efficient project planning and open-source contribution management.

## Features

* **Multi-Repository Support**: Monitor an unlimited number of public or private repositories.
* **Multi-Label Filtering**: Search for multiple labels (e.g., "good first issue", "help wanted") simultaneously.
* **Native YAML Integration**: Supports standard YAML list syntax for clean configuration.
* **UI Dashboard**: Outputs a formatted Markdown table directly to the GitHub Actions Step Summary.
* **GitHub CLI Powered**: Utilizes the native GitHub CLI for secure and efficient data retrieval.

## Implementation

### Basic Configuration

Create a file named `.github/workflows/issue-check.yml` in your repository.

```yaml
name: Contribution Dashboard
on:
  schedule:
    - cron: '0 15 * * *' # More info: https://crontab.guru/
  workflow_dispatch:

jobs:
  aggregate:
    runs-on: ubuntu-latest
    steps:
      - name: Aggregate Issues
        uses: issue/issue-finder@v1
        with:
          token: ${{ secrets.GITHUB_TOKEN }}
          repositories: |
            [
              "facebook/react",
              "vercel/next.js",
              "tailwindlabs/tailwindcss"
            ]
          labels: |
            [
              "good first issue",
              "help wanted"
            ]