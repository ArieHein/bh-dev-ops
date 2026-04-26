# OpsDB Component

## Component Name

- Name: OpsDB
- Domain: platform operational data store
- Owners: Azure DevTools Engineers, DevOps Lead and Architect
- Status: planned

## Purpose

- Problem solved: provide a provider-neutral persistent data store contract for configuration, routing,
  registrations, and workflow state used by platform components and services.
- Primary users: platform API, module workflows, and governance services.
- Workstreams impacted: all platform-managed workstreams.

## Implementation Scope (Current)

- Current version database engine: MongoDB.
- A dedicated MongoDB PowerShell module is currently used for operational automation.
- Core bootstrap collections are created at platform start for baseline configuration.

## Provider-Neutral Direction

- OpsDB component contracts must remain stable for callers regardless of backing database choice.
- Future database implementations should be swappable with minimal caller changes.
- Database-specific behavior should be isolated behind component and module boundaries.

## Platform Layer Coverage

- UI: management and diagnostics views consume API data backed by OpsDB.
- CLI: administrative and migration tasks executed through platform module commands.
- API: primary read and write access path for platform services.
- OpsDB usage: source of truth for platform configuration and module registry metadata.
- PowerShell module(s): current MongoDB module for collection bootstrap, schema validation, and data lifecycle
  tasks.
- MCP tool(s): optional MCP diagnostics and maintenance tools through approved API or module workflows.

## Core Bootstrap Collections (v1)

- `platform_config`
  - global and scoped configuration values
  - provider routing defaults and overrides
- `module_registry`
  - module registration metadata
  - module ownership, version, and lifecycle status
- `workflow_registry`
  - workflow definitions and activation state
  - workflow-to-module dependency declarations
- `request_log`
  - intake and execution request records
  - workflow correlation and status tracking

Collection names above are baseline placeholders and can be adjusted when full module structure is finalized.

## Security And Governance

- Authentication and authorization model: service identity and role-based access via platform API and controlled
  automation identities.
- Permission boundaries: direct write access restricted to approved automation paths.
- Governance module checks: schema validation, collection ownership, retention, and audit policy compliance.

## Testing And Quality

- Unit tests: module task commands and validation logic.
- Integration tests: API and workflow interactions with bootstrap collections.
- Security tests: authorization boundaries and sensitive configuration handling.
- Operational validation: startup bootstrap creates required collections idempotently.

## Dependency And Lifecycle

- Key dependencies (current): MongoDB runtime, platform API, OpsDB module workflows.
- Lifecycle status: planned.
- Upgrade and compatibility notes: concrete schema and indexing strategy are defined after prioritized module list
  and complete database model are provided.

## Persona Capability Coverage

| Capability | Workstream Product Owner | Workstream Developer | Workstream Manager | DevOps Team |
| --- | --- | --- | --- | --- |
| Query platform configuration (read) | no | no | no | yes |
| Manage module registry | no | no | no | yes |
| View workflow registry | no | no | no | yes |
| View request log | no | no | yes | yes |
