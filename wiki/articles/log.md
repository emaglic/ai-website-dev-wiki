# Project Log

This log records the chronological history of the project. Add entries after meaningful setup, design, content, development, wiki maintenance, lock cleanup, or deployment work.

## Entry Format

```markdown
## YYYY-MM-DD | type | Short description

- Summary:
- Files changed:
- Decisions:
- Follow-ups:
```

## 2026-06-07 | bootstrap | Created reusable website-wiki template

- Summary: Created the generic repository scaffold, starter wiki articles, repo-local setup workflow, and agent operating instructions.
- Files changed: `AGENTS.md`, `CLAUDE.md`, `.agents/`, `wiki/`, `site/`.
- Decisions: The `/setup` workflow is repo-local at `.agents/skills/setup/SKILL.md`; website implementation belongs in `site/`; project memory belongs in `wiki/articles/`.
- Follow-ups: Run `/setup` after cloning or starting a real website project.

