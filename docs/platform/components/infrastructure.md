# Web UI Infrastructure Component

## Purpose

- Present existing infrastructure and support infrastructure request workflows.

## Behavior

- Shows existing infrastructure across owned projects.
- Shows available infrastructure offerings for request.
  - mark the offering  with automated or manual fulfillment process.
- Allows environment definitions to be associated with infrastructure for discovery and request scoping.
- Supports requests for:
  - new Azure subscriptions
  - individual resources
  - complex multi-resource solutions
- Requested infrastructure is scoped to existing owned projects.

## Data And Integration

- Uses infrastructure inventory and infrastructure request APIs.
  - Some inventory data will be stored in OpsDB, some may be queried live from provider API.
- Records request status and related project scoping through platform services.

## Persona Capability Coverage

| Capability | Workstream Product Owner | Workstream Developer | Workstream Manager | DevOps Team |
| --- | --- | --- | --- | --- |
| View existing infrastructure | yes | yes | yes | yes |
| Request new Azure subscription | yes | no | no | yes |
| Request individual resources | yes | yes | no | yes |
| Request multi-resource solutions | yes | no | no | yes |
| Review and action infra requests | no | no | no | yes |
| View request status | yes | yes | yes | yes |
