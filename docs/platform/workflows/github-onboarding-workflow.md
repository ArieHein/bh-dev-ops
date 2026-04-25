# GitHub Onboarding Workflow Contract

This contract defines the orchestrated onboarding workflow for GitHub code and environment setup.

## Workflow Identifier

- Name: github-project-onboarding
- Trigger: PO request submitted from portal and approved by DevOps Lead
- Planner input: Product Owner allocates implementation time in planning cycle

## Input Contract

- Project name
- Naming convention key
- Workstream ID
- Product owner identity
- Member identities
- Existing workstream GitHub team reference, if any
- Optional environment name
- Optional subscription ID

## Execution Phases

1. Prechecks
   - validate request completeness
   - validate naming policy and role policy
   - validate all users are already invited to GitHub org (current version)
2. GitHub preparation
   - create repository
   - create or resolve GitHub team
3. Entra preparation
   - create Entra group
   - assign PO as owner
   - add members
4. Identity mapping
   - map GitHub team to Entra group
   - verify membership sync after propagation window
5. Repository access setup
   - assign default team role (normally `write`)
6. Optional environment and subscription setup
   - create OIDC-ready app registration
   - create repository environment
   - set environment secrets for tenant ID, subscription ID, client ID
   - assign Contributor role on subscription
7. Completion
   - persist status and generated IDs
   - return completion response to API

## Output Contract

- Repository URL and ID
- GitHub team ID
- Entra group ID
- Environment name, if requested
- App registration ID and client ID, if requested
- Workflow status and error details

## Rollback And Recovery

- Use compensating actions where safe and deterministic.
- Mark partially completed workflows as `needs-operator-review` with full trace details.

## Future Enhancement

- Commit starter workflow YAML that uses OIDC and environment scaffold.
