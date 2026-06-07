# Task Roadmap

This page tracks what has been done, what is next, and what is blocked.

## Current Status

- Template scaffold has been created.
- README now explains the base wiki project, directory structure, agent workflow, and `/setup` starting point.
- `.gitignore` now excludes temporary lock files, local environment files, dependencies, caches, generated outputs, logs, and OS/editor metadata.
- The repo-local `/setup` workflow is registered as a discoverable `setup` skill.
- Agent instructions now require a project-readiness preflight before project-specific work.
- Project-specific setup has not been run.

## Next Tasks

- Run `/setup` when ready to configure this template for a real website project.
- Add raw inspiration and content files to `wiki/raw/` if available.
- Initialize the website strategy, content direction, design direction, and technical approach in the wiki.
- Confirm in a fresh Codex session that the repo-local `setup` skill appears in skill discovery, or restart Codex if it does not.

## Backlog

- Define site structure after `/setup`.
- Build website files inside `site/` after project goals and technical approach are known.
- Ingest raw material from `wiki/raw/`.

## Completed Work

- Created generic wiki starter pages.
- Created repo-local setup workflow.
- Registered the setup workflow as a repo-local skill.
- Added project-readiness preflight rules to prevent project-specific work before the wiki contains enough real project context.
- Created agent instruction files.
- Created placeholder directories for raw material, local locks, and website files.
- Wrote the repository README for template users and future agents.
- Added repository ignore rules for non-source local and generated files.

## Blocked Items

- Project-specific planning and website development are blocked until `/setup` is run with real project details.
