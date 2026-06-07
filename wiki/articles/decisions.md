# Decisions

This page records durable project decisions so future agents understand what was chosen, why it was chosen, and what tradeoffs were considered.

## Decision Log Format

```markdown
## YYYY-MM-DD | Short decision title

- Decision:
- Rationale:
- Alternatives considered:
- Impact:
```

## 2026-06-07 | Use a repo-local setup workflow

- Decision: Store the `/setup` workflow at `.agents/skills/setup/SKILL.md`.
- Rationale: The template should remain portable and self-contained when cloned.
- Alternatives considered: Global or user-profile skills.
- Impact: Future agents should read the repo-local skill instead of requiring system-level configuration.

## 2026-06-07 | Separate wiki memory from website implementation

- Decision: Store project memory in `wiki/articles/` and website implementation in `site/`.
- Rationale: Separating knowledge management from implementation keeps both areas easier to maintain.
- Alternatives considered: Combining notes and site files in one directory.
- Impact: Future agents should update the wiki after meaningful work and keep website files inside `site/`.

