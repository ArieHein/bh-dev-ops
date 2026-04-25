# Decision Log

This file is the persistent source of truth for process, tooling, and team operating decisions.

## Decision Entry Format

- ID: DEC-XXXX
- Date: YYYY-MM-DD
- Status: proposed | accepted | superseded
- Owners: role names
- Context: why this decision is needed
- Decision: what was decided
- Impact: expected effects and tradeoffs
- Follow-up: actions required

## Entries

### DEC-0001

- Date: 2026-04-25
- Status: accepted
- Owners: Manager, DevOps Lead and Architect
- Context: New project needs a strict markdown-first collaboration standard.
- Decision: All markdown files must pass markdownlint with no issues before merge.
- Impact: Improves readability, consistency, and documentation quality.
- Follow-up: CI workflow and agent instructions must enforce this rule.

### DEC-0002

- Date: 2026-04-25
- Status: accepted
- Owners: Manager, DevOps Lead and Architect
- Context: Multi-agent team needs a baseline operating model before engineering rules are defined.
- Decision: Adopt the initial seven-agent structure and defer detailed responsibilities until DevOps Lead rules are provided.
- Impact: Team can begin coordinated work without locking in premature detailed standards.
- Follow-up: Update agent role files after engineering rules are supplied.

### DEC-0003

- Date: 2026-04-25
- Status: accepted
- Owners: DevOps Lead and Architect, Manager, Engineers
- Context: Tool and language choices require long-term maintainability and reliable adoption across teams.
- Decision: All 5 engineers must continuously track tool and framework ecosystems, version impact, language
  changes, package lifecycle, dependency reduction opportunities, and testing ecosystem implications.
- Impact: Improves resilience of technical choices and reduces unmanaged dependency and upgrade risk.
- Follow-up: Keep these checks explicit in future tooling and language ADR entries.

### DEC-0004

- Date: 2026-04-25
- Status: accepted
- Owners: DevOps Lead and Architect, Manager
- Context: Delivery practices need consistency and automation.
- Decision: Team operating model mandates CI, CD, continuous testing for quality and security, automated release
  management, and automated infrastructure provisioning with self-service configuration.
- Impact: Increases delivery reliability, auditability, and deployment speed.
- Follow-up: Add implementation roadmap items and automation milestones in planning artifacts.

### DEC-0005

- Date: 2026-04-25
- Status: accepted
- Owners: DevOps Lead and Architect, Manager, Product Owner
- Context: Team selected CALMS as the DevOps baseline and needs agent-specific adaptation.
- Decision: Adopt CALMS with explicit priorities on collaboration, engineer ownership, automation-first
  workflows, a measurement platform as one of the first tasks, and sharing through a platform blog section.
- Impact: Aligns technical and cultural practices with measurable outcomes and transparent learning.
- Follow-up: Track measurement platform scope and define initial metric set.

### DEC-0006

- Date: 2026-04-25
- Status: accepted
- Owners: DevOps Lead and Architect, Engineers
- Context: Cross-team language variation can block reuse and increase silo risk.
- Decision: Engineers must operate without silos, contribute to shared memory, and provide API, CLI, and MCP
  layers when one team's language is not shared by other teams. Maintain a central API registration location
  for discoverability plus shared modules and libraries.
- Impact: Improves interoperability, discoverability, and cross-team velocity.
- Follow-up: Define API registry structure and contribution workflow.

### DEC-0007

- Date: 2026-04-25
- Status: accepted
- Owners: Manager, DevOps Lead and Architect
- Context: Manager priorities are needed to guide execution quality across large multi-workstream delivery.
- Decision: Prioritize optimization across collaboration, automation, delivery, security, and support while
  preserving simplicity and maintainability.
- Impact: Strengthens delivery outcomes while reducing long-term operational complexity.
- Follow-up: Apply these optimization themes in tooling and platform decisions.

### DEC-0008

- Date: 2026-04-25
- Status: accepted
- Owners: Manager, Product Owner, DevOps Lead and Architect
- Context: DevOps capability must scale across 50 to 100 developers in 5 workstreams with mixed stacks.
- Decision: Establish structured enablement for mostly C# teams, plus frontend and data-science groups using
  Databricks and R.
- Impact: Increases consistent DevOps practices and reduces adoption gaps between workstreams.
- Follow-up: Define enablement assets and rollout sequence by workstream.

### DEC-0009

- Date: 2026-04-25
- Status: accepted
- Owners: Manager, DevOps Lead and Architect
- Context: Governance is required to support high-quality decisions and scalable operations.
- Decision: Use governance modules to support decision making and easy execution while improving permissions,
  performance, and cost outcomes.
- Impact: Creates predictable controls and improves execution confidence.
- Follow-up: Define governance module catalog and ownership.

### DEC-0010

- Date: 2026-04-25
- Status: accepted
- Owners: Manager, DevOps Lead and Architect, Engineers
- Context: Team collaboration cadence must be explicit and repeatable.
- Decision: Operate with daily software and DevOps collaboration, biweekly demos, and monthly updates with
  knowledge-sharing sessions.
- Impact: Improves transparency, alignment, and feedback speed.
- Follow-up: Create a recurring cadence calendar and facilitation checklist.

### DEC-0011

- Date: 2026-04-25
- Status: accepted
- Owners: DevOps Lead and Architect, Manager, Azure DevTools Engineers
- Context: Platform execution needs a clear baseline architecture for tool integration and operations.
- Decision: The platform architecture consists of UI, CLI, API, OpsDB under API, tool-specific PowerShell
  modules, and MCP tools that can call API or approved modules directly.
- Impact: Standardizes integration and operational implementation patterns across teams.
- Follow-up: Define concrete components and ownership once platform tool details are supplied.

### DEC-0012

- Date: 2026-04-25
- Status: accepted
- Owners: Manager, DevOps Lead and Architect, Engineers
- Context: Documentation consistency and discoverability are required for scaling platform operations.
- Decision: Each platform tool must have its own markdown document and be tracked in a central tools index,
  including API registration, module linkage, and MCP exposure.
- Impact: Improves maintainability, governance, onboarding speed, and cross-team reuse.
- Follow-up: Create initial tool documents and fill the platform tools index as details are provided.

### DEC-0013

- Date: 2026-04-25
- Status: accepted
- Owners: Product Owner Agent, Manager, DevOps Lead and Architect
- Context: The platform needs a concrete first tool definition for product-owner workflows.
- Decision: Define the first tool as a web-based UI focused on product owners, with dashboard, projects,
  people, services, and infrastructure tabs, plus left navigation to DevOps blog, support, and KB content.
- Impact: Establishes a clear user-facing baseline for platform interaction.
- Follow-up: Map this tool to concrete API routes and module implementations.

### DEC-0014

- Date: 2026-04-25
- Status: accepted
- Owners: Product Owner Agent, Manager, DevOps Lead and Architect
- Context: Project visibility and collaboration behavior require explicit policy.
- Decision: Project visibility defaults to private invite-only access; project owners may mark projects internal
  for cross-product-owner visibility. Favorites are supported and shown on dashboard with a configured cap.
- Impact: Balances privacy controls with selective discoverability and operational usability.
- Follow-up: Define exact favorite cap policy and enforcement behavior.

### DEC-0015

- Date: 2026-04-25
- Status: accepted
- Owners: Product Owner Agent, Azure DevTools Engineers, DevOps Lead and Architect
- Context: The UI needs clear people, service, and infrastructure operations tied to platform governance.
- Decision: People tab uses Microsoft Entra users by default, marks memberships and roles, and allows project
  owner invite plus role assignment. Services and infrastructure tabs support request workflows that route
  intake forms to DevOps for review, planning, and implementation.
- Impact: Standardizes onboarding, role assignment, and request intake patterns across projects.
- Follow-up: Define request form schemas, workflow states, and DevOps response SLAs.

### DEC-0016

- Date: 2026-04-25
- Status: accepted
- Owners: Azure DevTools Engineers, DevOps Lead and Architect, Product Owner Agent
- Context: A concrete GitHub onboarding flow is required for code and environment setup at project start.
- Decision: Adopt a GitHub onboarding workflow that creates repository and team, provisions and maps Entra
  group, assigns default team role, and optionally configures OIDC app registration plus environment secrets
  when subscription and environment details are requested.
- Impact: Reduces onboarding variation and creates a repeatable automation baseline.
- Follow-up: Implement API and module command set for each workflow phase.

### DEC-0017

- Date: 2026-04-25
- Status: accepted
- Owners: DevOps Lead and Architect, Azure DevTools Engineers
- Context: Workflow orchestration spans multiple systems and needs modular execution boundaries.
- Decision: Use module-level task commands and module-level workflow scripts for GitHub and Entra, plus a main
  orchestration workflow script that coordinates both modules and records progress in OpsDB.
- Impact: Improves maintainability, reuse, and failure isolation.
- Follow-up: Define naming conventions and contracts for task commands and orchestration script APIs.

### DEC-0018

- Date: 2026-04-25
- Status: accepted
- Owners: DevOps Lead and Architect, Manager
- Context: Current onboarding scope has known assumptions and future enhancements.
- Decision: Current version assumes all requested users are already invited to GitHub org. Later versions add
  user invite automation and commit a baseline workflow YAML that uses OIDC and environment configuration.
- Impact: Enables immediate delivery while preserving a clear evolution path.
- Follow-up: Schedule invite automation and baseline YAML generation in next planning cycles.

### DEC-0019

- Date: 2026-04-25
- Status: accepted
- Owners: DevOps Lead and Architect, Azure DevTools Engineers
- Context: Workloads should be resilient to provider changes and avoid direct vendor coupling.
- Decision: Adopt provider-neutral module buffer pattern where workflows call neutral commands such as
  `Get-PlatformVM`, while provider adapters encapsulate vendor-native cmdlets or APIs.
- Impact: Reduces migration effort and improves maintainability of workload scripts.
- Follow-up: Define neutral command catalog and normalized contracts for prioritized capability areas.

### DEC-0020

- Date: 2026-04-25
- Status: accepted
- Owners: DevOps Lead and Architect, Azure DevTools Engineers, Network and Security Engineers
- Context: Provider selection can vary by context such as DNS zone and should be resolved consistently.
- Decision: Use config-driven provider routing from OpsDB with optional explicit provider override in request.
  DNS routing example uses zone mapping to choose between Azure DNS and ClouDNS adapters.
- Impact: Enables flexible multi-provider operation while preserving a stable caller experience.
- Follow-up: Define OpsDB routing schema, approval flow, and audit requirements for routing changes.

### DEC-0021

- Date: 2026-04-25
- Status: accepted
- Owners: Manager, DevOps Lead and Architect, Azure DevTools Engineers
- Context: Engineering examples should not be treated as immediate implementation backlog before priorities are
  explicitly provided.
- Decision: Existing module and routing examples are reference patterns only. Concrete module command catalogs,
  implementation contracts, and delivery sequencing are deferred until prioritized module list and database
  design input are provided.
- Impact: Prevents premature implementation and keeps execution aligned with approved priorities.
- Follow-up: Update module docs with production contracts after priority list and database details are received.

### DEC-0022

- Date: 2026-04-25
- Status: accepted
- Owners: DevOps Lead and Architect, Azure DevTools Engineers, Manager
- Context: Platform requires an initial operational database choice for first implementation phase.
- Decision: Use MongoDB as OpsDB engine for version 1 and provide a dedicated MongoDB PowerShell module.
- Impact: Establishes a consistent starting point for configuration, registry, and workflow state persistence.
- Follow-up: Refine data model and validation rules when full module structure is provided.

### DEC-0023

- Date: 2026-04-25
- Status: accepted
- Owners: DevOps Lead and Architect, Azure DevTools Engineers
- Context: Platform startup requires baseline collections to support immediate configuration and registration
  capabilities.
- Decision: Create core bootstrap collections at startup, including configuration and module registration
  collections, with naming and schema finalized in the upcoming database design phase.
- Impact: Enables controlled initialization and deterministic platform startup behavior.
- Follow-up: Define final collection schema, indexes, and retention model from detailed database input.

### DEC-0024

- Date: 2026-04-25
- Status: accepted
- Owners: Manager, DevOps Lead and Architect
- Context: Platform naming and documentation anchor are required for consistent communication.
- Decision: Official platform name is `Beehive`, and a dedicated Beehive platform overview page is maintained
  to capture DevOps Lead and Architect platform ideas.
- Impact: Improves naming consistency and creates a single location for platform vision.
- Follow-up: Populate Beehive overview page with DevOps Lead and Architect principles and roadmap guidance.

### DEC-0025

- Date: 2026-04-25
- Status: accepted
- Owners: Manager, DevOps Lead and Architect, Azure DevTools Engineers
- Context: Markdown policy tooling needs to scale beyond lint rules to include additional checks such as spelling
  and grammar.
- Decision: Move markdown lint configuration under `.github/tools/markdown` and require CI and local commands
  to use the explicit config path from that folder.
- Impact: Creates an extensible policy-tooling location under `.github` and reduces future migration effort when
  additional markdown quality tools are added.
- Follow-up: Add spelling and grammar check configurations and workflows under `.github/tools/markdown` when
  tool selection is finalized.

### DEC-0026

- Date: 2026-04-25
- Status: accepted
- Owners: Manager, DevOps Lead and Architect, Azure DevTools Engineers
- Context: Markdown policy expansion requires a concrete spelling checker selection and enforceable automation.
- Decision: Adopt `cspell` as the markdown spelling checker, with configuration stored at
  `.github/tools/markdown/cspell.json` and CI enforcement via `.github/workflows/markdown-spelling.yml`.
- Impact: Introduces consistent spelling quality checks in markdown and establishes an extensible path for future
  grammar tooling.
- Follow-up: Add grammar checker evaluation and implementation in a separate decision entry.

### DEC-0027

- Date: 2026-04-25
- Status: accepted
- Owners: Manager, DevOps Lead and Architect, Engineers
- Context: Engineering expectations need explicit documentation ownership, and spelling vocabulary growth needs
  cleaner structure.
- Decision: Require all engineers to write and maintain documentation as a baseline responsibility, and split
  cspell vocabulary into dedicated dictionary files under `.github/tools/markdown/dictionaries/`.
- Impact: Improves documentation accountability and keeps spelling policy vocabulary maintainable as the
  platform grows.
- Follow-up: Continue expanding dictionaries by domain and review dictionary terms during PRs that add tooling.
