# Web UI Services Component

## Purpose

- Present the service catalog and capture service request workflows.

## Behavior

- Shows service catalog entries grouped by category.
- Initial examples include Azure services like subscriptions and code services like GitHub.
- Includes request flow for adding new services to existing projects.
- New service request submission opens an intake form routed to DevOps team review and planning.

## Data And Integration

- Uses services catalog and service request APIs.
- Records request status through platform services and OpsDB-backed workflows.

## Persona Capability Coverage

| Capability | Workstream Product Owner | Workstream Developer | Workstream Manager | DevOps Team |
| --- | --- | --- | --- | --- |
| View service catalog | yes | yes | yes | yes |
| Submit service request | yes | yes | no | no |
| Review and action service requests | no | no | no | yes |
| View request status | yes | yes | yes | yes |
