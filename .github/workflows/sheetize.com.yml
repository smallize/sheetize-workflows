name: Build sheetize.com

on:
  workflow_dispatch:

jobs:
  trigger-com-workflows:
    runs-on: ubuntu-latest
    steps:
      - name: List all .com.yml workflows
        id: list
        run: |
          find .github/workflows -name '*.com.yml' > com_workflows.txt
          cat com_workflows.txt

      - name: Install GitHub CLI
        uses: cli/cli@v3

      - name: Trigger all .com.yml workflows with environment production
        env:
          GH_TOKEN: ${{ secrets.GITHUB_TOKEN }}
        run: |
          while read workflow; do
            # Get the workflow file name only
            wf_name=$(basename "$workflow")
            echo "Dispatching $wf_name with environment=production"
            gh workflow run "$wf_name" -f environment=production
          done < com_workflows.txt
