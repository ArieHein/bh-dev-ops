# Platform Personas

This document defines the platform personas, their goals, and the specific functionality available to
each persona across platform components and services. It is a living document updated by the DevOps
team as new capabilities are delivered.

## How To Use This Document

- Each persona section describes who the persona is, what they are trying to accomplish, and how the
  platform supports them.
- Component documents define persona capability coverage for each component.
- Availability values:
  - `yes` - available
  - `no` - not available
  - `read-only` - can view but not change
  - `planned` - approved for delivery, not yet live
  - `n/a` - not applicable to this persona

## Ownership And Maintenance

- This document is owned and maintained by the DevOps Product Owner.
- New capability rows are added by the DevOps Product Owner with input from all five engineers and
  support from the DevOps Manager.
- Persona definitions and capability assignments are reviewed whenever a new platform feature is
  delivered or a new role is introduced.
- Keeping this document current is a standing responsibility of the DevOps Product Owner role.

---

## Personas

### Workstream Roles

These personas represent users who belong to software delivery workstreams and consume platform
capabilities to manage projects, people, services, and infrastructure.

#### Workstream Product Owner

**Who**: leads one or more software delivery workstreams and owns the project portfolio for their teams.

**Platform goals**:

- Discover and manage projects across workstreams.
- Invite engineers and assign project roles.
- Request new platform services and infrastructure.
- Track project metrics and delivery status.
- Manage project visibility for cross-team collaboration.

#### Workstream Developer

**Who**: a developer, data scientist, or engineer working within a workstream product owner's project.

**Platform goals**:

- View project details and membership for projects they belong to.
- Access repositories, workflows, and environments set up for their projects.
- Request new workflows and tooling through defined intake flows.
- Use platform CLI and MCP tools for day-to-day automation and delivery tasks.

#### Workstream Manager

**Who**: owns delivery operations, team priorities, and cross-workstream alignment for one or more workstreams.

**Platform goals**:

- Track delivery velocity and team metrics across owned workstreams.
- Review platform adoption and service usage.
- Support decision-making with aggregate project and team data.

### DevOps Roles

These personas belong to the DevOps team and are responsible for platform health, governance, and
service delivery.

#### DevOps Lead and Architect

**Who**: defines technical direction, approves workflows, and owns platform health across all workstreams.

**Platform goals**:

- Approve and govern workflow requests submitted by engineers and product owners.
- Monitor platform-wide health, usage, and service status.
- Manage platform services, module catalog, and OpsDB configuration.
- Define and update platform standards across the team.

---

## Component-Level Capability Source

Persona capability matrices are maintained in each component document to avoid duplication and keep
capabilities close to component behavior:

- `docs/platform/components/dashboard.md`
- `docs/platform/components/projects.md`
- `docs/platform/components/people.md`
- `docs/platform/components/services.md`
- `docs/platform/components/infrastructure.md`
- `docs/platform/components/github-code-workflows-component.md`
- `docs/platform/components/opsdb-component.md`
- `docs/platform/components/config.md`

---

## Adding New Capabilities

When a new platform capability is released:

1. DevOps Product Owner collects input from all five engineers and the DevOps Manager on capability
  scope and persona access boundaries.
2. Identify the component the capability belongs to.
3. Add or update capability rows in the relevant component document with `yes`, `no`, `read-only`, or
  `planned` per persona.
4. If a persona is added, removed, or changed by the DevOps Product Owner, update persona capability
  coverage in each component document where that persona is applicable.
5. If a new persona is introduced, add a persona section under the appropriate role group above.
6. Record the change in `docs/decisions/decision-log.md` if the feature reflects a governance or
   architecture decision.
