# GitHub Code And Workflows Component

## Component Name

- Name: GitHub Code And Workflows
- Domain: repository lifecycle and onboarding automation
- Owners: Azure DevTools Engineers, DevOps Lead and Architect
- Status: planned

## Purpose

- Problem solved: standardize onboarding for projects that need GitHub repositories, teams, identity mapping,
  and environment-ready deployment access.
- Primary users: DevOps team, product owners, and project engineers.
- Workstreams impacted: all workstreams using GitHub code and workflow automation.

## Platform Layer Coverage

- UI: request is initiated from platform portal and includes PO-provided project and membership details.
- CLI: PowerShell-based execution for module commands and orchestrated workflows.
- API: receives onboarding request payload and tracks status for each execution stage.
- OpsDB usage: stores request metadata, workflow execution state, generated identifiers, and approval audit trail.
- PowerShell module(s): GitHub module and Entra module with task commands plus composable workflow scripts.
- MCP tool(s): onboarding orchestration tool that calls API and workflow scripts.

## Onboarding Workflow: GitHub Project Setup

This workflow is proposed by engineers, approved by DevOps Lead, and planned by Product Owner.

### Preconditions

- GitHub organization exists and is integrated with Entra group sync.
- Request contains project details from portal, including:
  - project name
  - workstream context
  - PO identity
  - member list
  - optional subscription and environment request
- For current version, assume all requested users are already invited to GitHub org.

### Workflow Steps

1. Create repository using project name and approved naming convention.
2. Create a GitHub team for the repository unless a workstream team already exists.
3. Create an Entra group, make the PO owner, and add PO-provided members.
4. Validate all users already exist in GitHub organization membership.
5. Map the GitHub team to the Entra group so synced members appear after propagation delay.
6. Assign default repository role to team, expected default is `write` unless policy overrides.
7. If request includes subscription for a specific environment:
   - create app registration with OIDC trust bound to GitHub repo and requested environment name
   - create matching repository environment
   - create environment secrets for tenant ID, subscription ID, and client ID
   - grant app registration identity Contributor on target subscription

### Future Version Scope

- Add baseline workflow YAML commit with minimal deployment scaffold for environment and OIDC usage.

## Module And Script Architecture

### GitHub Module

- Scope: individual GitHub tasks.
- Example task commands:
  - create repository
  - create team
  - assign team role to repository
  - create repository environment
  - set environment secrets
- Composable workflow script: GitHub onboarding workflow composed from task commands.

### Entra Module

- Scope: individual Entra tasks.
- Example task commands:
  - create Entra group
  - assign group owner
  - add group members
  - create app registration with federated identity credential for OIDC
- Composable workflow script: Entra onboarding workflow composed from task commands.

### Main Orchestration Workflow

- Scope: cross-module coordination and transaction-style progress control.
- Behavior:
  - calls GitHub and Entra workflow scripts in approved sequence
  - applies prechecks and policy validations
  - records each stage in OpsDB
  - reports status back to platform API

## API And Module Mapping

- API endpoints used:
  - onboarding request create
  - onboarding status query
  - approval state update
- Module commands used:
  - GitHub module task commands and workflow script
  - Entra module task commands and workflow script
  - main orchestration workflow script
- Direct MCP-to-module usage, if any:
  - Justification: permitted for operational automation when API mediation is not required.
  - Security and audit notes: execution must log actor, request ID, command scope, and outcome.

## Security And Governance

- Authentication and authorization model: Entra-backed identity with role-based authorization.
- Permission boundaries:
  - PO can request and provide onboarding details
  - DevOps Lead approves workflow and policy-critical actions
  - automation identities execute constrained module actions
- Governance module checks:
  - naming convention policy
  - role assignment policy
  - environment and subscription policy
  - OIDC and app registration policy

## Testing And Quality

- Unit tests: each module task command and validation function.
- Integration tests: full onboarding workflow against test organization and test subscription.
- Security tests: role assignment scope, secret handling, and OIDC trust validation.
- Operational validation: successful sync of Entra group members to GitHub team after mapping.

## Reliability And Operations

- Observability requirements:
  - per-step execution metrics
  - retries and failure causes
  - sync delay tracking for Entra to GitHub propagation
- Support runbook links: pending runbooks.
- Known risks and mitigations:
  - Risk: sync delay may hide membership immediately after mapping.
  - Mitigation: show expected propagation window and include delayed verification checks.

## Dependency And Lifecycle

- Key dependencies: GitHub org config, Entra integration, subscription RBAC automation, platform API, OpsDB.
- Lifecycle status: planned.
- Upgrade and compatibility notes:
  - current version assumes pre-invited GitHub users
  - later versions include user invite automation and baseline workflow file commit

## Persona Capability Coverage

| Capability | Workstream Product Owner | Workstream Developer | Workstream Manager | DevOps Team |
| --- | --- | --- | --- | --- |
| View repository details | yes | yes | yes | yes |
| Initiate project onboarding request | yes | no | no | yes |
| Propose new workflow | no | yes | no | yes |
| Approve workflow request | no | no | no | yes |
| Allocate workflow to planning | yes | no | no | no |
| View onboarding status | yes | yes | no | yes |
