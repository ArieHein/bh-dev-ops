# Beehive Platform Architecture

This document defines the base architecture for Beehive and its current and future tools.

## Core Platform Layers

- UI layer for human interaction and operational workflows.
- CLI layer for automation, scripting, and developer usage.
- API layer for system integration and platform orchestration.
- OpsDB under the API as the operational data store for platform management.
- PowerShell module layer under the API, organized by tool and platform domain.
- MCP server layer exposing tools that can call the API or directly call approved modules.

## OpsDB Engine (v1)

- MongoDB is the first-version OpsDB engine.
- A dedicated MongoDB PowerShell module manages bootstrap and operational tasks.
- Core baseline collections are created at startup for configuration and registry concerns.

## Required Flow Patterns

- Preferred flow: MCP tool to API to OpsDB or module.
- Allowed direct flow: MCP tool to approved module when justified by latency, reliability, or execution model.
- Every direct-to-module path must be documented with security, auditability, and support implications.

## Tool Documentation Requirement

- Every platform tool must have its own markdown document.
- Each tool document must describe UI touchpoints, CLI command surface, API endpoints, module mapping,
  OpsDB dependencies, and MCP tool exposure.
- Tool documents must include ownership, lifecycle status, and testing strategy.

## PowerShell Module Organization

- Modules are grouped by tool and platform domain.
- Module naming must be consistent and discoverable.
- Module functions must document API linkage and MCP usage expectations.

## Provider-Neutral Buffer Pattern

- Workloads and workflows must call provider-neutral commands, not vendor-native commands directly.
- Neutral commands route to provider adapters using request input or configuration resolved from OpsDB.
- Neutral command contracts remain stable even if provider implementation changes.
- Provider adapters encapsulate vendor-native cmdlets or APIs.
- This pattern reduces migration impact when providers are replaced.

Examples:

- `Get-PlatformVM` routes to VMware or Azure implementations.
- `New-PlatformDnsRecord` routes by zone-to-provider mapping.

## MCP Integration Rules

- MCP tools may use API endpoints by default.
- MCP tools may call modules directly only for explicitly approved scenarios.
- MCP tool contracts must specify authentication, authorization, error handling, and telemetry behavior.

## Next Planning Inputs

- Platform, tools, and practice details from stakeholders.
- API registration model and service discovery structure.
- Initial governance module catalog.

## Current Tool Design Input: Web UI

- UI type: web-based system.
- Persona: product owner of software teams across workflows.
- Main dashboard shows owned projects and project metrics.
- Visibility model:
  - default project visibility is private and invite-only
  - project owner may mark a project internal for cross-PO visibility
- Projects tab supports filtering, search, and favorites with a configured favorite limit.
- People tab shows platform users from Microsoft Entra by default, marks existing project members with roles,
  and supports invite plus role assignment by project owners.
- Services tab shows categorized services, supports add-service requests, and routes intake forms to DevOps.
- Infrastructure tab shows existing infrastructure and requestable offerings, including subscriptions,
  individual resources, and multi-resource solutions.
- Left navigation includes access to DevOps blog, support pages, and knowledge-base articles.

## Current Component Design Input: GitHub Code And Workflows

- Request lifecycle: engineers suggest workflow, DevOps Lead approves, Product Owner allocates planning time.
- Onboarding flow includes:
  - repository creation with naming convention
  - GitHub team creation or workstream team reuse
  - Entra group creation with PO as owner and requested members
  - Entra-to-GitHub team mapping through configured sync
  - default repository role assignment, expected `write`
  - optional OIDC app registration and environment setup for subscription requests
- Integration assumptions and future scope:
  - current version assumes users are already invited to GitHub org
  - future version adds invite automation and baseline workflow YAML commit
- Module orchestration pattern:
  - GitHub module for task commands plus module workflow script
  - Entra module for task commands plus module workflow script
  - main workflow script calls module workflows and tracks status

## Current Module Design Input: Provider Routing

- DNS requests use neutral commands and route by zone mapping in OpsDB.
- Example mapping:
  - `example.com` -> `cloudns`
  - `example-dev.com` -> `azuredns`
- Azure DNS adapter wraps Azure DNS cmdlets.
- ClouDNS adapter wraps provider API operations.

## Current Component Design Input: MongoDB OpsDB

- First version uses MongoDB as operational database.
- MongoDB PowerShell module is required for bootstrap, validation, and maintenance tasks.
- Core collections are initialized at startup, including configuration and module registration collections.
