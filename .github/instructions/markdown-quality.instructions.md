---
applyTo: "**/*.md"
description: "Enforce markdown lint quality for all markdown content. Use when creating or editing markdown, READMEs, decision logs, or agent docs."
---

# Markdown Quality Gate

- Every markdown file must pass markdownlint with no warnings or errors.
- Write markdown that is lint-clean on first draft when possible.
- Keep headings ordered and avoid skipping heading levels.
- Use a single `#` heading per file unless the document is intentionally embedded content.
- Wrap long prose lines to a practical readable width (target 120 characters based on repo config).
- Use consistent list formatting and spacing.
- Keep code fences typed where possible, for example `bash`, `yaml`, or `json`.
- Avoid trailing spaces and duplicate headings in the same section scope.
- Do not use hard tabs in markdown content; use spaces for indentation and wrapped lines.

## Active markdownlint Rules

These rules are configured in `.github/tools/markdown/markdownlint-cli2.jsonc`.

| Rule ID | Purpose | Common Value |
| --- | --- | --- |
| `MD013` | line length | `line_length: 120`, `code_blocks: false`, `tables: false` |
| `MD004` | unordered list marker style | `style: dash` |
| `MD007` | unordered list indentation | `indent: 2`, `start_indented: false` |
| `MD009` | trailing spaces policy | `br_spaces: 2`, `strict: false` |
| `MD010` | hard tab handling | `code_blocks: false`, `spaces_per_tab: 2` |
| `MD022` | heading surrounding blank lines | `lines_above: 1`, `lines_below: 1` |
| `MD024` | duplicate heading behavior | `siblings_only: true` |
| `MD025` | single top-level heading | `level: 1` |
| `MD029` | ordered list style | `style: one_or_ordered` |
| `MD030` | list marker spacing | `ul_single: 1`, `ol_single: 1`, `ul_multi: 1`, `ol_multi: 1` |
| `MD031` | fenced code block padding | `true` |
| `MD032` | list surrounding blank lines | `true` |
| `MD033` | inline HTML policy | `false` |
| `MD034` | bare URL policy | `false` |
| `MD041` | first line heading policy | `true` |

## Rule Documentation Notes

- Prefer explicit rule IDs in discussions, issues, and PR reviews, for example `MD013` or `MD024`.
- Use `MD010` as the enforcement anchor for hard-tab detection and keep it enabled.
- When changing rule values, update both the config and this document in the same change.
- If a rule must be relaxed, record the reason in the decision log.

Quick tab scan before finalizing:

```bash
rg "[\\x09]" --glob "**/*.md"
```

Before finalizing markdown changes, validate locally with:

```bash
npx markdownlint-cli2 --config .github/tools/markdown/markdownlint-cli2.jsonc "**/*.md"
```

If linting fails, fix the markdown instead of suppressing rules unless there is a strong reason
documented in a decision record.
