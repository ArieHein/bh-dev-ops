# DevOps Multi-Agent Team Structure

## Team Composition

- 1 Manager
- 1 Product Owner
- 2 Engineers focused on network and security
- 2 Engineers focused on Azure management and developer tools
- 1 DevOps Lead and Architect

## Decision Model

- Tool decisions are co-owned by the Manager and DevOps Lead.
- All team members provide input before a tool decision is finalized.
- Final decisions are recorded in the decision log before they are treated as active standards.

## Current Phase

- Phase 1: Foundation and structure.
- DevOps Lead rules are now active and define cross-team engineering behavior.

## Collaboration Rules

- Product Owner defines business outcomes and acceptance criteria.
- Engineers contribute technical implementation options and risks.
- DevOps Lead sets technical direction and quality standards.
- Manager resolves conflicts and keeps delivery aligned with goals.

## Organization Context

- The operating model supports 50 to 100 developers across 5 workstreams.
- Most developers are C#, with additional frontend and data-science groups.
- Data-science workflows include Databricks and R usage that must be integrated into DevOps standards.

## Manager Priorities

- Optimize delivery operations across collaboration, automation, delivery, security, and support.
- Grow internal DevOps knowledge and expertise across all workstreams.
- Keep standards simple for long-term maintainability.
- Enforce good-practice adoption through repeatable playbooks.
- Apply governance modules that support decision quality, execution speed, permissions, performance,
  and cost control.
- Scale DevOps capabilities to accelerate software delivery velocity.

## Collaboration Cadence

- Daily collaboration between software teams and the DevOps team.
- Biweekly progress demos every 2 weeks.
- Monthly updates and formal knowledge-sharing sessions.

## Engineering Capability Rules

- All 5 engineers must maintain working knowledge of every approved tool and framework.
- Engineers continuously track language and framework releases and assess impact before adoption.
- Engineers must monitor package lifecycle to reduce unnecessary dependencies and avoid stale packages.
- Engineers evaluate and test emerging practices with practical, working scenarios.
- Every tool and language decision must include an explicit testing ecosystem plan.
- Every engineer must write and maintain documentation for owned capabilities, workflows, and standards.

## DevOps Delivery Rules

- Continuous Integration and Continuous Deployment are mandatory operating practices.
- Continuous testing for quality and security is required in every delivery workflow.
- Release management must be automated.
- Infrastructure provisioning and self-service configuration must be automated.

## CALMS Adaptation For Agents

- Culture: enforce collaboration and no-silo behavior across all engineering roles.
- Automation: automate the majority of operational and delivery activities.
- Lean: reduce manual handoffs and unnecessary dependencies.
- Measurement: build a team measurement platform as one of the first implementation tasks.
- Sharing: publish early learnings in a blog section within the platform.

## Shared Memory And Interoperability

- Engineers maintain role-specific memory and contribute to shared team memory.
- Knowledge must be discoverable across teams and not kept in local silos.
- If one team writes code in a language another team does not use, interoperability layers are required.
- Required interoperability layers include API, CLI, and MCP interfaces where relevant.
- A central API registration location is required for service discovery and shared module and library usage.

## Platform Baseline Architecture

- The platform standard includes UI, CLI, API, OpsDB, tool-level PowerShell modules, and MCP tools.
- OpsDB is positioned under the API as the operational data layer.
- API and module capabilities must be exposed through MCP tools where agent usage is needed.
- MCP tools should call API endpoints by default.
- Direct MCP-to-module calls are allowed only when explicitly approved and documented.
- Each platform tool must maintain its own markdown document.
