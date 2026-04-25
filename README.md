# BeeHive DevOps Foundation

DevOps multi-agent project foundation.

## Platform Name

- Official platform name: Beehive

## Current Focus

- Establish markdown-first operating standards.
- Create baseline team agent structure.
- Record durable decisions for use across sessions.

## Markdown Linting Policy

All markdown in this repository must be lint-clean.

- Lint rules are in `.github/tools/markdown/markdownlint-cli2.jsonc`.
- Spelling rules are in `.github/tools/markdown/cspell.json`.
- Spelling dictionaries are in `.github/tools/markdown/dictionaries/`.
- CI enforcement is in `.github/workflows/markdown-lint.yml` and `.github/workflows/markdown-spelling.yml`.
- Authoring instructions are in `.github/instructions/markdown-quality.instructions.md` and
  `.github/instructions/markdown-spelling.instructions.md`.

Run locally before commit:

```bash
npx markdownlint-cli2 --config .github/tools/markdown/markdownlint-cli2.jsonc "**/*.md"
npx cspell lint --config .github/tools/markdown/cspell.json "**/*.md"
```

## Agent Team Baseline

Team structure is defined in `docs/team/TEAM-STRUCTURE.md` and role files under `.github/agents/`:

- Manager
- Product Owner
- Network Security Engineer 1
- Network Security Engineer 2
- Azure DevTools Engineer 1
- Azure DevTools Engineer 2
- DevOps Lead and Architect

Engineering operating rules are now active and documented in `docs/team/TEAM-STRUCTURE.md`.

## Active Operating Model

- All 5 engineers must continuously track ecosystem changes, version impact, package lifecycle, and testing
  practices for each approved tool or language.
- Team delivery follows CI, CD, continuous testing for quality and security, automated release management,
  and automated infrastructure provisioning with self-service configuration.
- CALMS adaptation is active, including collaboration, ownership, automation-first delivery, and an early
  measurement platform with a blog section for shared learning.
- Teams avoid silos by contributing to shared memory and exposing API, CLI, and MCP interfaces when language
  boundaries limit direct code reuse.
- Manager priorities are active: optimize collaboration, automation, delivery, security, and support while
  keeping standards simple and maintainable.
- Operating context includes 50 to 100 developers across 5 workstreams, mostly C#, plus frontend and
  data-science teams working with Databricks and R.
- Collaboration cadence is active: daily software and DevOps collaboration, biweekly demos, and monthly
  update and knowledge-sharing sessions.

## Persistent Decision Records

Use `docs/decisions/decision-log.md` as the source of truth for accepted decisions.

- Decision recording behavior is enforced by `.github/instructions/decision-recording.instructions.md`.
- Operating model behavior is reinforced by `.github/instructions/engineering-operating-model.instructions.md`.
- Use `docs/decisions/adr-template.md` for drafting major decisions.

## Platform Architecture Docs

- Beehive platform overview page: `docs/platform/BEEHIVE.md`
- Platform baseline architecture: `docs/platform/PLATFORM-ARCHITECTURE.md`
- Per-tool documentation template: `docs/platform/TOOL-DOCUMENT-TEMPLATE.md`
- Platform tool registry index: `docs/platform/PLATFORM-TOOLS-INDEX.md`
- Platform web UI component overview: `docs/platform/components/WEB-UI.md`
- Platform web UI component docs: `docs/platform/components/`
- GitHub component spec: `docs/platform/components/GITHUB-CODE-WORKFLOWS.md`
- GitHub onboarding workflow contract: `docs/platform/workflows/github-onboarding-workflow.md`
- Provider-neutral module pattern: `docs/platform/modules/PROVIDER-NEUTRAL-MODULE-PATTERN.md`
- DNS provider routing pattern: `docs/platform/modules/DNS-PROVIDER-ROUTING.md`
- OpsDB MongoDB component spec: `docs/platform/components/OPSDB-MONGODB.md`
