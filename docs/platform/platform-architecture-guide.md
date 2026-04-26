# Beehive Platform Architecture

This document defines the base architecture for Beehive, its service model, and integration patterns.

## Architectural Concepts

### Tools vs Services

- A **tool** is a strategic decision to use an external or foundational capability (GitHub, MongoDB, Azure).
- A **service** is a platform abstraction layer that wraps one or more tools and exposes stable, provider-neutral
  interfaces for other platform components and users.
- Example: GitHub tool provides Repository and Workflow services. Beehive exposes these as unified service
  abstractions that include all orchestration (teams, environments, secrets) and carry stable caller contracts.

### Service Dual-Interface Model

Every service provides:

1. **PowerShell Module Interface** (CLI-based): Task-oriented commands for automation, scripting, and
   orchestration workflows.
2. **API Interface** (HTTP-based): RESTful or RPC endpoints that call the underlying module, enabling UI,
   MCP, and non-PowerShell integrations to consume the service.

Both interfaces are registered in OpsDB so platform components can discover and use them.

### Service Registration and Plugin Pattern

- Each service registers itself in OpsDB with metadata: name, module name, API endpoint, ownership, and
  lifecycle status.
- Services act as plugins connected to Beehive through a central API router that dispatches calls to the
  appropriate service module or API.
- Service registration allows dynamic discovery and orchestration across the platform.

## Core Platform Layers

- **Interface Layer** with UI, CLI, and MCP entry points.
- **API Layer** with a central API contract that routes requests to services and acts as the primary
  orchestration and integration point.
- **Service Layer** with platform services such as Repository, Workflow, Access Management, Logging,
  Metrics, Identity, OpsDB, and additional domain services. Each service owns:
  - A PowerShell module for CLI/workflow automation
  - An API endpoint (served by central API)
  - Registration metadata in OpsDB
- **Data Layer** hosting OpsDB as the operational data store, service registry, and configuration source.
- **Integration Layer** hosting external integrations such as Teams and AI Agent that call the API or
  services.

## OpsDB Engine (v1)

- MongoDB is the first-version OpsDB engine.
- A dedicated MongoDB PowerShell module manages bootstrap and operational tasks.
- Core baseline collections are created at startup for configuration and registry concerns.

## Architecture Rendering Contract

**Visual Layout Constraints** (for diagrams and architecture visualization):

- Interface Layer renders at **top center**.
- API Layer renders at **center**.
- Service Layer renders at **bottom center**.
- Data Layer renders at **left of API Layer**.
- Integration Layer renders at **right of API Layer**.

**Allowed Flow Connectors**:

- Primary flow: Interface Layer → API Layer → Service Layer (solid arrows).
- Side connections: Data Layer ↔ API Layer (solid lines); Integration Layer ↔ API Layer (solid lines).
- MCP bridge: MCP (from Interface) ⇢ CLI, MCP ⇢ API (dashed lines for approved direct-access scenarios).

**Forbidden Direct Connections** (unless explicitly approved):

- Interface Layer → Data Layer (all access through API).
- Interface Layer → Integration Layer (all access through API).
- Interface Layer → individual Service boxes (access only through API abstraction).

## Required Flow Patterns

- **Primary execution flow**: Interface Layer → API Layer → Service Layer.
- **Service call chain**: Interface entry point → API → service module or API endpoint → OpsDB (as needed).
- **MCP access paths**: MCP can reach services via:
  - Direct module calls (approved scenarios, dashed lines in diagram)
  - API via PowerShell HTTP client
  - API via standard HTTP
  - All paths are logged and audited.
- **Integration Layer**: Teams, AI Agent, and other external integrations typically call API Layer for
  platform interactions.
- **Data Layer**: OpsDB is accessed only through service modules or the API layer, never directly from
  Interface, MCP, or Integration layers.

## Service Documentation Requirement

- Every platform service must have its own markdown component document.
- Each service document must describe:
  - Service name, domain, and ownership.
  - Tool(s) wrapped by this service (if any).
  - PowerShell module interface: command names, inputs, outputs, and error handling.
  - API interface: endpoint paths, request/response contracts, and error codes.
  - OpsDB registration metadata and discovery contract.
  - UI, CLI, and MCP integration touchpoints.
  - Security boundaries and governance checks.
  - Lifecycle status and upgrade compatibility notes.
- A separate tool-level summary document may be created if a tool wraps multiple services or has
  orchestration workflows.

## PowerShell Module Organization

- One module per service (or per logical service domain if a service has multiple sub-domains).
- Module name must match service name: `Beehive.Service.<ServiceName>` pattern.
- Module registration is persisted in OpsDB so CLI automation and the API layer can discover and invoke
  modules dynamically.
- Module functions must document:
  - Their purpose and inputs/outputs.
  - Whether they are stable public APIs or internal helpers.
  - Any OpsDB dependencies.
  - MCP usage expectations if exposed to MCP tools.
- The API layer calls module functions to serve HTTP endpoints, so modules must remain independent of HTTP
  transport concerns.

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

MCP tools have three legitimate access paths to platform services:

1. **Direct Module Call** (PowerShell-to-PowerShell):
   - MCP calls service module functions directly (dashed line in architecture diagram).
   - Approved for scenarios requiring low latency, direct workflow orchestration, or handling large result
     sets.
   - Must be documented in service specs with security and auditability justification.
   - Requires MCP runtime to support PowerShell execution.

2. **API via PowerShell** (PowerShell HTTP client):
   - MCP calls the API Layer using PowerShell HTTP clients (`Invoke-RestMethod`, etc.).
   - Provides uniform interface while maintaining PowerShell compatibility.
   - Recommended when MCP is PowerShell-based but API routing is preferred.

3. **API via HTTP** (Standard REST/RPC):
   - MCP calls API endpoints using standard HTTP clients (curl, Node.js, Python, etc.).
   - Preferred path for non-PowerShell MCP implementations and external integrations.
   - Preferred for UI, external agents, and Language Model integrations.

All MCP access paths must:

- Specify authentication, authorization, error handling, and telemetry behavior in MCP tool contract.
- Log all access with request ID, actor identity, and path taken (module, API, etc.) for auditability.
- Respect service-level rate limits and circuit-breaker policies defined in service specs.

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
