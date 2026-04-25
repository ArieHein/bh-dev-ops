---
applyTo: "**"
description: "Record team process, tooling, and architectural decisions in the persistent decision log. Use when decisions are proposed, accepted, or changed."
---

# Decision Recording Requirement

- Record only material, durable decisions that change team workflow, tool selection, governance, standards,
  platform architecture, ownership, or delivery policy.
- Record decision updates in `docs/decisions/decision-log.md`.
- Use the decision entry format for substantial decisions that are likely to matter across sessions.
- Do not add decision log entries for routine documentation edits, wording refinements, lint rule housekeeping,
  formatting fixes, or other low-level implementation adjustments unless they materially change policy.
- Tool decisions require ownership by both the Manager and DevOps Lead and includes team input summary.
- If a previous decision changes, mark the old entry as superseded and add a new decision entry.
- Decisions are not active standards until written in the decision log.
