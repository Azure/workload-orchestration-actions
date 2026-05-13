# WO: Deploy

Deploy a Solution Template Version to a Workload Orchestration Target.

This action reviews, publishes, and installs a solution template version on the specified target using the Azure CLI `workload-orchestration` extension.

## Inputs

| Name | Description | Required |
|------|-------------|----------|
| `solution-template-version-id` | Full Azure resource ID of the solution template version | Yes |
| `target-id` | Full Azure resource ID of the target | Yes |

### Expected resource ID formats

- **Solution Template Version**: `/subscriptions/{subscriptionId}/resourceGroups/{resourceGroup}/providers/Microsoft.Edge/solutionTemplates/{solution}/versions/{version}`
- **Target**: `/subscriptions/{subscriptionId}/resourceGroups/{resourceGroup}/providers/Microsoft.Edge/targets/{target}`

## Prerequisites

- The runner must be authenticated with Azure CLI (`az login`).
- `jq` must be available on the runner.

## Usage

```yaml
- uses: Azure/workload-orchestration-actions/deploy@main
  with:
    solution-template-version-id: /subscriptions/.../solutionTemplates/mySolution/versions/1.0.0
    target-id: /subscriptions/.../targets/myTarget
```
