# Platform Web UI

This document defines the Beehive platform web UI as a platform component rather than a standalone tool.

## Purpose

- Provide product owners one web experience to discover, manage, and request project-related platform
  capabilities.
- Act as the primary human-facing UI component for platform workflows.

## Ownership

- Owners: Product Owner Agent, Manager Agent, Azure DevTools Engineers
- Status: planned

## Component Model

- The web UI is a platform component composed of focused UI areas.
- Each major UI area is documented in its own markdown file under `docs/platform/components/`.

## Component Documents

- Dashboard: `docs/platform/components/dashboard.md`
- Projects: `docs/platform/components/projects.md`
- People: `docs/platform/components/people.md`
- Services: `docs/platform/components/services.md`
- Infrastructure: `docs/platform/components/infrastructure.md`

## Shared Platform Coverage

- UI: web application with left navigation and component-focused workflows.
- API: required for project, people, service, and infrastructure interactions.
- OpsDB usage: stores project metadata, visibility, favorites, memberships, requests, and status.
- PowerShell module(s): platform modules for project, membership, service catalog, and infrastructure actions.
- MCP tool(s): MCP tools for project queries, membership operations, and request workflows.

## Shared Navigation

- Left navigation menu provides access to:
  - dashboard
  - projects
  - people
  - services
  - infrastructure
  - DevOps blog
  - support and knowledge-base articles

## Security And Governance

- Authentication and authorization model: Microsoft Entra authentication with role-based authorization.
- Permission boundaries: project-owner scope controls invitation, role assignment, and request permissions.
- Governance module checks: visibility policy, role assignment policy, request workflow policy, and approval
  policy.

## Testing And Quality

- Unit tests: UI components, navigation logic, visibility rules, and validation.
- Integration tests: UI to API flows for projects, people, services, and infrastructure.
- Security tests: authorization checks for private and internal visibility and role assignment flows.

## Reliability And Operations

- Observability requirements: page usage metrics, request success rates, invitation events, and failure tracking.
- Support runbook links: pending platform runbooks.

## Dependency And Lifecycle

- Key dependencies: Microsoft Entra, API platform, OpsDB, service catalog modules, infrastructure modules.
- Lifecycle status: planned.
- Upgrade and compatibility notes: maintain backward-compatible API contracts for UI and CLI clients.
