# Workload Orchestration Actions

- [Workload Orchestration Actions](#workload-orchestration-actions)
  - [Actions](#actions)
    - [Deploy](#deploy)
  - [Prerequisites](#prerequisites)
  - [Usage](#usage)
    - [Deploy a Solution Template](#deploy-a-solution-template)
  - [Reference](#reference)
    - [Input Formats](#input-formats)

With [Workload Orchestration Actions](https://github.com/Azure/workload-orchestration-actions), you can manage [Workload Orchestration](https://learn.microsoft.com/en-us/azure/azure-arc/workload-orchestration/) resources through GitHub Actions.

## Actions

### Deploy

Deploy a Solution Template to a Workload Orchestration Target. This action deploys a solution templates version on the specified target.

| Input | Description | Required |
|-------|-------------|----------|
| `solution-template-version-id` | Full Azure resource ID of the Solution Template Version | Yes |
| `target-id` | Full Azure resource ID of the Target | Yes |

## Prerequisites

- The runner must be authenticated with Azure CLI ([`azure/login`](https://github.com/Azure/login)).
- `jq` must be available on the runner.

## Usage

### Deploy a Solution Template

```yaml
name: Deploy Solution Template

on:
  workflow_dispatch:

permissions:
  id-token: write
  contents: read

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - name: Azure Login
        uses: azure/login@v2
        with:
          client-id: ${{ secrets.AZURE_CLIENT_ID }}
          tenant-id: ${{ secrets.AZURE_TENANT_ID }}
          subscription-id: ${{ secrets.AZURE_SUBSCRIPTION_ID }}

      - name: Deploy to Target
        uses: Azure/workload-orchestration-actions/deploy@v1
        with:
          solution-template-version-id: ${{ vars.SOLUTION_TEMPLATE_VERSION_ID }}
          target-id: ${{ vars.TARGET_ID }}
```

## Reference

### Input Formats

| Input | Format | Example |
|-------|--------|---------|
| `solution-template-version-id` | `/subscriptions/{sub}/resourceGroups/{rg}/providers/Microsoft.Edge/solutionTemplates/{name}/versions/{version}` | `/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myRg/providers/Microsoft.Edge/solutionTemplates/mySolution/versions/1.0.0` |
| `target-id` | `/subscriptions/{sub}/resourceGroups/{rg}/providers/Microsoft.Edge/targets/{target}` | `/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myRg/providers/Microsoft.Edge/targets/myTarget` |
