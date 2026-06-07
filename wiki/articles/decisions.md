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

- Decision: Store the `/setup` workflow as an actual repo-local skill at `.agents/skills/setup/SKILL.md`.
- Rationale: The template should remain portable and self-contained when cloned while still allowing Codex skill discovery where supported.
- Alternatives considered: Global or user-profile skills; instruction-only workflow without skill frontmatter.
- Impact: Future agents should read the repo-local skill instead of requiring system-level configuration. Users may ask for `/setup` naturally or invoke the `setup` skill directly where available.

## 2026-06-07 | Require setup before project-specific work

- Decision: Agents must check whether the wiki has enough project-specific information before doing project-specific website, content, design, wiki strategy, or site implementation work.
- Rationale: The starter wiki is intentionally generic and should not be treated as initialized project memory merely because files exist.
- Alternatives considered: Letting agents infer project details from partial prompts; relying only on a setup log entry; relying only on placeholder detection.
- Impact: If the starter articles are still boilerplate, lack the minimum project definition, or show setup has not run, agents should tell the user the project needs `/setup` and ask whether to run it now. If the wiki is partially initialized but missing task-relevant information, agents should ask focused follow-up questions or offer to resume `/setup`. Template-maintenance work can still proceed before setup.

## 2026-06-07 | Separate wiki memory from website implementation

- Decision: Store project memory in `wiki/articles/` and website implementation in `site/`.
- Rationale: Separating knowledge management from implementation keeps both areas easier to maintain.
- Alternatives considered: Combining notes and site files in one directory.
- Impact: Future agents should update the wiki after meaningful work and keep website files inside `site/`.

## 2026-06-07 | Add post-setup research memory

- Decision: Add `wiki/articles/research.md` for synthesized research findings and `wiki/raw/research/` for user-provided research sources. Project-specific research should happen only after `/setup` captures the project field, audience, goals, and expert perspective.
- Rationale: Useful research depends on knowing the website context and should become durable project memory only when it meaningfully affects strategy, content, design, SEO, positioning, technical choices, or future decisions.
- Alternatives considered: Store research in existing content or inspiration pages; create a separate research skill immediately; allow research before setup.
- Impact: Future agents should answer research questions as domain experts after setup, cite web/current claims, avoid blindly cataloging search results, and ask the user before filing findings whose relevance is unclear.
