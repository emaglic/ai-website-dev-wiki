# AI Website Dev Wiki

This repository is a reusable base project for building websites with AI assistance and a persistent markdown wiki.

It starts intentionally generic. The idea is to give an AI coding agent a stable place to store project memory, source material, decisions, design direction, technical notes, and the actual website files as the project evolves.

## What This Template Is For

Use this project when you want to build a website with an AI assistant while keeping durable context inside the repository.

The wiki helps future agent sessions understand:

- what website is being built
- who it is for
- what content and inspiration have been provided
- what design and technical decisions have already been made
- what work is done, next, blocked, or unresolved

This avoids restarting from scratch every time a new AI session begins.

## Project Structure

```text
.
├── .agents/
│   ├── locks/              # Temporary coordination locks for agent work
│   └── skills/setup/       # Repo-local /setup workflow
├── site/                   # Website implementation files
├── wiki/
│   ├── articles/           # LLM-managed project wiki
│   └── raw/
│       ├── content/        # User-provided raw content
│       ├── inspiration/    # Visual references, screenshots, palettes, examples
│       └── research/       # Market, competitor, audience, SEO, and industry sources
├── AGENTS.md               # Operating instructions for AI agents
├── CLAUDE.md               # Companion agent instructions
└── README.md
```

## How The Wiki Works

The `wiki/articles/` folder is project memory managed by AI agents. Agents should read it before doing meaningful work and update it after meaningful work.

Key pages include:

- `wiki/articles/index.md`: map of the wiki
- `wiki/articles/project-brief.md`: website goals, audience, pages, and constraints
- `wiki/articles/design-direction.md`: visual strategy and inspiration
- `wiki/articles/content-inventory.md`: content sources, missing copy, and content risks
- `wiki/articles/technical-architecture.md`: chosen stack, deployment assumptions, and build notes
- `wiki/articles/research.md`: synthesized research findings and expert guidance
- `wiki/articles/task-roadmap.md`: current status, next tasks, backlog, and blocked items
- `wiki/articles/decisions.md`: durable decisions and rationale
- `wiki/articles/open-questions.md`: unresolved questions
- `wiki/articles/log.md`: chronological project history

The `wiki/raw/` folder is for user-provided source material. Treat these files as source-of-truth input. Agents should not modify raw files unless explicitly asked.

Research uses two layers: `wiki/raw/research/` stores user-provided research sources, while `wiki/articles/research.md` stores only meaningful synthesized findings. Project-specific research should wait until `/setup` has defined the project field, audience, goals, and expert perspective.

## Getting Started With `/setup`

When you are ready to turn this generic template into a real website project, ask your AI agent to run:

```text
/setup
```

The repo-local setup workflow lives at:

```text
.agents/skills/setup/SKILL.md
```

It is also registered as a repo-local Codex skill, so Codex surfaces that support skills may show it as `setup` or let you invoke it as `$setup`.

During `/setup`, the agent will ask focused questions about:

- the kind of website you are building
- who or what the site is for
- the target audience and primary goal
- needed pages or sections
- available content and inspiration
- available research sources and the expert perspective agents should use
- visual direction and brand constraints
- preferred technical approach and hosting needs

After that, the agent initializes the wiki with project-specific strategy, content notes, design direction, technical choices, open questions, and a roadmap.

Do not personalize this template for a specific website before running `/setup`. If an agent sees that the wiki is still mostly boilerplate or lacks the basic project definition needed for the task, it should pause project-specific work and ask whether you want to run `/setup` first.

## Building The Website

Website implementation belongs in `site/`.

Unless the project needs a framework or special tooling, the default recommendation is simple static HTML, CSS, and JavaScript. That keeps the site portable, fast, and easy to deploy through basic hosting or FTP.

Future agents should choose the simplest technical architecture that satisfies the project goals and document that choice in `wiki/articles/technical-architecture.md`.

## Working With AI Agents

Agents should follow `AGENTS.md` before making meaningful changes. In short:

- read the wiki first
- check `wiki/raw/` for relevant source material
- coordinate edits to `wiki/articles/` and `site/` with `.agents/locks/`
- keep wiki updates concise and useful
- record durable decisions and progress
- keep website work inside `site/`

This makes the repository useful across multiple sessions, tools, and agents.

## Typical Workflow

1. Add any raw copy, notes, references, screenshots, or brand material to `wiki/raw/`.
2. Ask the agent to run `/setup`.
3. Review the initialized wiki and answer any open questions.
4. Build the website inside `site/`.
5. Keep the wiki updated as the project changes.

## Current State

This repository is currently a base template. Project-specific planning and website development should begin with `/setup`.
