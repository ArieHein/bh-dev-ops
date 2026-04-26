---
applyTo: "**/*.md"
description: "Enforce cspell spelling checks for markdown content. Use when creating or editing markdown documents."
---

# Markdown Spelling Gate

- Every markdown file must pass cspell checks with no unknown words unless explicitly approved in cspell config.
- Prefer adding team or platform-specific terms to `.github/tools/markdown/dictionaries/` rather than
  suppressing findings inline.
- Keep custom word list focused and review it when new terms are introduced.

Before finalizing markdown changes, validate locally with:

```bash
npx cspell lint --config .github/tools/markdown/cspell.json "**/*.md"
```

If spelling checks fail, fix spelling first and only then extend approved vocabulary when the term is valid.
