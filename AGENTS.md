# Website Wiki Template Agent Guide

This repository is a reusable template for building websites with AI assistance and a persistent LLM-managed markdown wiki. It is intentionally generic. Do not personalize it for a specific website until the user asks to run `/setup`.

## Core Structure

- `wiki/raw/` contains user-provided source material. Treat these files as source-of-truth input and do not modify them unless the user explicitly asks.
- `wiki/raw/inspiration/` contains design references, screenshots, mood boards, color palettes, layout references, component inspiration, and other visual material.
- `wiki/raw/content/` contains raw content such as resumes, bios, project descriptions, service notes, copy drafts, or brand material.
- `wiki/articles/` contains the LLM-managed project wiki. Agents own these files and must keep them current.
- `site/` contains the actual website. Put HTML, CSS, JavaScript, assets, framework code, and build files here unless there is a strong project-specific reason otherwise.
- `.agents/skills/setup/SKILL.md` contains the repo-local `/setup` workflow.
- `.agents/locks/` contains temporary repo-local coordination locks for concurrent agent work.

## Before Meaningful Work

Before doing meaningful website, content, design, or strategy work:

1. Read `wiki/articles/index.md`.
2. Read `wiki/articles/log.md`.
3. Read relevant wiki articles such as `project-brief.md`, `design-direction.md`, `content-inventory.md`, `technical-architecture.md`, `task-roadmap.md`, `decisions.md`, and `open-questions.md`.
4. Check `wiki/raw/` for new source material when the task involves content or design direction.
5. Check `.agents/locks/` before editing files in `wiki/articles/` or `site/`.

## After Meaningful Work

After doing meaningful work:

1. Update affected wiki articles.
2. Add durable decisions to `wiki/articles/decisions.md`.
3. Update `wiki/articles/task-roadmap.md`.
4. Append a chronological entry to `wiki/articles/log.md`.
5. Update `wiki/articles/index.md` if wiki pages were created, renamed, removed, or meaningfully changed.

## Repo-Local `/setup`

When the user asks for `/setup`, read and follow `.agents/skills/setup/SKILL.md`.

The `/setup` workflow is intentionally repo-local and portable. Do not install, create, or require global, system-wide, user-profile, or machine-level skills for this template.

## Wiki Maintenance Standards

Keep wiki articles concise, structured, and useful to future agents. Use markdown headings, bullet lists, cross-links, and dated entries where helpful.

When information comes from raw source files, mention the source file. When something is an agent inference, label it as an inference.

Do not let the wiki become a transcript. Synthesize important context, decisions, open questions, risks, and progress.

## Website Development Standards

All website implementation work goes inside `site/`.

Choose the simplest technical architecture that satisfies the project goals. If the user does not have a strong preference and no special requirements exist, prefer static HTML, CSS, and JavaScript for portability and easy FTP deployment.

Prioritize clear content hierarchy, a strong first impression, mobile responsiveness, fast loading, accessible markup, maintainable structure, visual consistency, and realistic content usage.

When inspiration exists in `wiki/raw/inspiration/`, use it to inform layout, visual tone, typography, color, spacing, and interaction choices. When content exists in `wiki/raw/content/`, adapt it into website-ready copy instead of copying raw material verbatim unless that is clearly appropriate.

## User Collaboration

Assume users may not be developers. Explain technical choices in plain language, ask focused questions when needed, and handle implementation work directly.

Once the website type and industry are known, act as an expert in that domain as well as a wiki manager and website developer. Help make the website strategically better, not merely technically complete.

## Concurrency And File Locks

Agents may work in parallel on this repository. Coordinate before editing files in `wiki/articles/` or `site/` by using repo-local lock files in `.agents/locks/`. Do not use global lock files or system-level coordination.

Before editing `wiki/articles/` or `site/`:

1. Identify the files or directories you expect to modify.
2. Check `.agents/locks/` for active locks that overlap those paths.
3. If an overlapping lock exists, do not edit those files. Report the conflict and ask the user whether to wait, switch tasks, or inspect the stale lock.
4. If no overlapping lock exists, create a lock file in `.agents/locks/`.
5. Keep the lock scope as narrow as possible.

Use this lock file naming pattern:

```text
.agents/locks/YYYYMMDD-HHMMSS-agent-name.lock
```

Use this lock file format:

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

While working:

- Do not modify files outside your declared lock scope unless you first update or create an appropriate lock.
- For broad work, prefer multiple narrow locks over one vague repository-wide lock.
- Keep lock files short-lived.
- Refresh `Last heartbeat` and `Expires` when a task runs longer than expected.
- Default lock expiration should be short, usually 30 to 60 minutes, unless the user explicitly approves longer-running work.
- If another agent changed a file you planned to edit, stop and reconcile before writing.

After finishing:

1. Update the relevant wiki articles and `wiki/articles/log.md`.
2. Remove your lock file.
3. Report what changed.

If a lock appears stale:

- Inspect `Created`, `Last heartbeat`, `Expires`, and `Scope`.
- If the `Expires` time has not passed, treat the lock as active.
- If the `Expires` time has passed, treat the lock as stale.
- Before removing or overriding a stale lock, check whether there are uncommitted or unexpected file changes in the locked scope.
- If locked files contain changes that may belong to an interrupted agent, preserve them and ask the user how to proceed.
- If the lock is stale and there are no conflicting file changes in scope, the agent may remove it and must record that cleanup in `wiki/articles/log.md`.

This lock protocol is cooperative rather than foolproof. It makes coordination visible and reduces accidental overwrites.

