---
applyTo: "**"
description: "Apply DevOps engineering operating model rules for CALMS, no-silo collaboration, interoperability layers, and lifecycle-driven tooling decisions."
---

# Engineering Operating Model

- Treat DevOps Lead rules as active standards across all team workflows.
- For every tool and language decision, include:
  - release cadence and version impact review
  - package lifecycle and dependency minimization review
  - testing ecosystem and continuous testing strategy
- Enforce CI, CD, continuous quality testing, and continuous security testing.
- Require automated release management and automated infrastructure provisioning.
- Require self-service configuration for engineering teams where practical.
- Optimize operating outcomes across collaboration, automation, delivery, security, and support.
- Favor simplicity and maintainability for process and platform decisions.
- Use governance modules and checkpoints that improve decision quality, execution speed, permissions,
  performance, and cost management.
- Apply practices across mixed workstream profiles, including C#, frontend, Databricks, and R teams.
- Scale DevOps platform capabilities to accelerate delivery across all workstreams.
- Follow CALMS adaptation:
  - collaboration and engineer ownership first
  - automation as default for most workflows
  - measurement platform as an early deliverable
  - sharing via platform blog content
- Maintain collaboration rhythm:
  - daily software and DevOps collaboration
  - biweekly progress demos
  - monthly updates and knowledge-sharing sessions
- Enforce no-silo operation:
  - keep role-specific memory and contribute to shared memory
  - design API, CLI, and MCP layers when language boundaries block adoption
  - maintain a central API registration location for discoverability
- Enforce platform architecture baseline:
  - platform uses UI, CLI, API, OpsDB, tool-specific PowerShell modules, and MCP tools
  - each platform tool must have its own markdown document
  - MCP tools call API by default and may call modules directly only when approved and documented
  - workflows call provider-neutral platform commands, not vendor-native commands directly
  - provider resolution may be explicit in request or resolved from OpsDB configuration
  - persona definitions are owned by DevOps Product Owner in `docs/platform/platform-personas-guide.md`
  - when DevOps Product Owner changes personas, update persona capability coverage in each applicable
    component document under `docs/platform/components/`

