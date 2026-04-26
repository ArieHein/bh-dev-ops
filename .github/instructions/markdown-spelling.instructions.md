---
applyTo: "**/*.md"
description: "Enforce cspell spelling checks for markdown content. Use when creating or editing markdown documents."
---

# Markdown Spelling Gate

- Use en-US spelling for markdown content to avoid en-GB and en-US variation drift.
- Every markdown file should pass cspell checks with no unknown words unless explicitly approved in cspell config.
- Prefer adding team or platform-specific terms to `.github/tools/markdown/dictionaries/` rather than
  suppressing findings inline.
- Keep custom word list focused and review it when new terms are introduced.
- PR behavior for spelling is informational only for now and should not block merges.

Before finalizing markdown changes, validate locally with:

```bash
npx cspell lint --config .github/tools/markdown/cspell.json "**/*.md"
```

If spelling checks fail, fix spelling first and only then extend approved vocabulary when the term is valid.
