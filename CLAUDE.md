# Website Wiki Template Guide For Claude

This repository is a reusable template for building websites with AI assistance and a persistent LLM-managed markdown wiki. It is generic by design. Do not personalize it for a specific website until the user asks to run `/setup`.

## Repository Map

- `wiki/raw/` contains user-provided source material. Treat these files as source-of-truth input and do not modify them unless explicitly asked.
- `wiki/raw/inspiration/` contains design references, screenshots, mood boards, color palettes, layout references, component inspiration, and other visual material.
- `wiki/raw/content/` contains raw content such as resumes, bios, project descriptions, service notes, copy drafts, or brand material.
- `wiki/raw/research/` contains user-provided research sources such as market notes, competitor lists, PDFs, articles, links, audience notes, SEO material, and industry context.
- `wiki/articles/` contains the LLM-managed project wiki. Agents maintain these files as the project memory.
- `site/` contains the actual website. Put all implementation files here unless the project wiki documents a strong reason otherwise.
- `.agents/skills/setup/SKILL.md` contains the repo-local `/setup` workflow.
- `.agents/locks/` contains temporary repo-local coordination locks.

## Operating Rhythm

Before meaningful work, read `wiki/articles/index.md`, `wiki/articles/log.md`, and the wiki pages relevant to the task. Check `wiki/raw/` when the task involves content, design direction, or research.

Before project-specific website, content, design, research, wiki strategy, or site implementation work, verify whether the wiki has enough project-specific information to proceed. Read the starter project articles: `project-brief.md`, `design-direction.md`, `content-inventory.md`, `technical-architecture.md`, `research.md`, `task-roadmap.md`, `open-questions.md`, `log.md`, and `decisions.md`. Treat setup as incomplete when the wiki is still boilerplate or lacks a minimum project definition: website type, owner or brand, industry or field, expert perspective for research and strategy, primary goal, target audience, likely pages or sections, chosen stack or deployment assumption, and a setup log entry. Placeholder-heavy starter articles or a roadmap saying setup has not been run mean setup is incomplete. If setup is incomplete, tell the user the project wiki still needs `/setup` and ask whether they want to run it now. If the wiki is partially initialized but lacks information needed for the current task, ask focused follow-up questions or offer to resume `/setup`. Template-maintenance work may proceed before setup when the user is explicitly improving the template itself.

After meaningful work, update the affected wiki articles, record durable decisions in `wiki/articles/decisions.md`, update `wiki/articles/task-roadmap.md`, append to `wiki/articles/log.md`, and update `wiki/articles/index.md` when wiki pages change meaningfully.

## Repo-Local `/setup`

When the user asks for `/setup`, or explicitly invokes the repo-local `setup` skill, read and follow `.agents/skills/setup/SKILL.md`.

The `/setup` workflow is an actual repo-local skill at `.agents/skills/setup/SKILL.md`. It must remain checked into this repository so the template can be cloned and reused without global, system-wide, user-profile, or machine-level skill files.

## Wiki Standards

The wiki is project memory, not a transcript. Keep articles concise, structured, cross-linked, and useful to future agents.

When information comes from raw source files, mention the source file. When something is an inference, label it as an inference.

## Research Standards

Project-specific research should happen only after `/setup` has initialized the project wiki, because setup defines the website type, field, audience, goals, and expert lens. When the user asks research-related questions after setup, act as an expert in the relevant documented field and preserve only meaningful synthesized findings in `wiki/articles/research.md`.

Support both user-provided source material from `wiki/raw/research/` and web/current research when appropriate. Do not blindly catalog search results. Cite sources for web/current claims, label agent inference, note confidence or uncertainty, and ask the user before filing findings whose relevance is unclear.

Use `wiki/raw/research/` for market, competitor, audience, SEO, industry, and source-document research. Use `wiki/raw/inspiration/` for visual and design references.

## Website Standards

All website work belongs in `site/`.

Choose the simplest technical architecture that satisfies the project goals. If the user has no strong preference and no special requirements exist, default toward static HTML, CSS, and JavaScript for portability and easy FTP deployment.

Prioritize clear hierarchy, strong first impression, mobile responsiveness, fast loading, accessibility, maintainability, visual consistency, and realistic content.

Use `wiki/raw/inspiration/` to inform design decisions. Use `wiki/raw/content/` to adapt raw material into website-ready copy.

## Working With Users

Assume users may not be developers. Explain choices in plain language, ask focused questions when needed, and handle implementation directly.

Once the website type and industry are known, act as an expert in that domain. Give strategic guidance as well as technical implementation.

## Concurrency And Locking

Before editing `wiki/articles/` or `site/`, coordinate with repo-local lock files in `.agents/locks/`. Do not use global or system-level locks.

Before editing:

1. Identify the files or directories you expect to modify.
2. Check `.agents/locks/` for active locks that overlap those paths.
3. If an overlapping lock exists, do not edit those files. Report the conflict and ask the user whether to wait, switch tasks, or inspect the stale lock.
4. If no overlapping lock exists, create a lock file in `.agents/locks/`.
5. Keep the lock scope as narrow as possible.

Lock file name:

```text
.agents/locks/YYYYMMDD-HHMMSS-agent-name.lock
```

Lock file format:

```markdown
# Agent Work Lock

- Agent: <agent name or session id>
- Created: <YYYY-MM-DD HH:MM timezone>
- Last heartbeat: <YYYY-MM-DD HH:MM timezone>
- Expires: <YYYY-MM-DD HH:MM timezone>
- Scope:
  - <path/to/file-or-directory>
- Purpose: <short description>
- Expected release: <short estimate>
```

While working, do not modify files outside the lock scope unless you first update or create a suitable lock. Keep locks short-lived, usually 30 to 60 minutes. Refresh `Last heartbeat` and `Expires` if work runs longer than expected.

After finishing, update the wiki, append the log, remove the lock file, and report what changed.

If a lock appears stale, inspect `Created`, `Last heartbeat`, `Expires`, and `Scope`. If the expiration has not passed, treat it as active. If it has passed, check for uncommitted or unexpected changes in scope before removing it. Preserve possible interrupted-agent work and ask the user how to proceed when conflicts are unclear. If stale cleanup is safe, record it in `wiki/articles/log.md`.

This protocol is cooperative rather than foolproof. It is meant to make coordination visible and reduce accidental overwrites.
