# Website Wiki Template Agent Guide

This repository is a reusable template for building websites with AI assistance and a persistent LLM-managed markdown wiki. It is intentionally generic. Do not personalize it for a specific website until the user asks to run `/setup`.

## Provider-Neutral Instructions

This file is the authoritative repository guide for every agent tool and provider. `CLAUDE.md`, `GEMINI.md`, and any future tool-specific entry files are small adapters that direct agents here; do not duplicate the rules into separate provider guides.

Keep reusable workflows in `.agents/skills/`. Native skill discovery, command syntax, repository access, browser tools, and delegation depend on the actual application and version, not just the model provider. Read the requested `SKILL.md` explicitly if native invocation is unavailable. A request to read and run `.agents/skills/setup/SKILL.md` is equivalent to invoking `/setup`; merely reading instructions or adapting an agent tool is not permission to initialize the wiki.

During user-requested setup, follow the setup skill's agent adaptation step. Keep adaptations repo-local, preserve existing user configuration and adapters for other tools, and leave shared rules unchanged when switching tools. Adding support for another agent later must not reset project knowledge or rerun website initialization. Reviewers may use a different provider from the requesting agent; give them the same requirements and shared instructions, using manual handoff where needed.

## Core Structure

- `input/assets/` and `input/mockups/` are mutable, disposable user working directories for website assets and design mockups, including Figma exports. Their contents may change or disappear at any time.
- `temp/` is an ephemeral handoff area for user-provided screenshots, draft proposals, and other temporary material. Users may delete its contents at any time.
- `output/` contains ephemeral files explicitly requested by the user for human consumption, such as reports or implementation plans. Website development files belong in `site/`.
- `wiki/raw/` contains user-provided source material. Treat these files as source-of-truth input and do not modify them unless the user explicitly asks.
- `wiki/raw/inspiration/` contains design references, screenshots, mood boards, color palettes, layout references, component inspiration, and other visual material.
- `wiki/raw/content/` contains raw content such as resumes, bios, project descriptions, service notes, copy drafts, or brand material.
- `wiki/raw/research/` contains user-provided research sources such as market notes, competitor lists, PDFs, articles, links, audience notes, SEO material, and industry context.
- `wiki/articles/` contains the LLM-managed project wiki. Agents own these files and must keep them current.
- `wiki/temp/` contains ephemeral agent-generated working files, including review briefs and feedback. Contents are ignored by Git except `.gitkeep`.
- `site/` contains the actual website. Put HTML, CSS, JavaScript, assets, framework code, and build files here unless there is a strong project-specific reason otherwise.
- `.agents/skills/setup/SKILL.md` contains the repo-local `/setup` workflow.
- `.agents/skills/self-review/SKILL.md` contains the repo-local independent code-review workflow.
- `.agents/skills/uiux-self-review/SKILL.md` contains the repo-local independent UI/UX review workflow.
- `.agents/locks/` contains temporary repo-local coordination locks for work in `site/`. Wiki articles use modification checks and merging instead of locks.

## Mutable Design Inputs

Use `input/` for the user's evolving design workspace; use top-level `temp/` for one-off handoffs. Only `input/assets/.gitkeep` and `input/mockups/.gitkeep` are tracked; other contents, including additional subdirectories, are ignored by Git.

- Reinspect relevant inputs when asked to use them; do not assume they match a previously viewed version.
- Copy assets needed by the website into appropriate subdirectories under `site/`. Website code must reference those copies, never files in `input/`. Leave user originals intact unless explicitly asked to move, edit, or delete them.
- Use mockups to guide implementation. If a particular version is valuable as a lasting reference, copy it into `wiki/raw/inspiration/` with a descriptive version-specific filename, without overwriting retained references. Preserve useful conclusions in the appropriate wiki articles.
- Wiki articles must never link to files in `input/` or rely on their continued availability. Cite retained copies under `site/` or `wiki/raw/` when source references are needed. Tell the user which files were copied and where.
- Follow existing setup readiness and concurrency rules for project-specific work. The presence of design inputs does not authorize running `/setup`.

## Human-Requested Deliverables

Write files to `output/` when the user requests a human-readable deliverable, such as a project report, analysis, or implementation plan, unless they specify another destination. Tell the user where the deliverable was saved.

- `output/` is not a development workspace. All website code, styles, scripts, assets, configuration, build files, and other site development files belong in `site/`. A request to build or change the website does not mean to place development files in `output/`.
- Internal agent working files belong in `wiki/temp/`; `output/` is for user-requested files intended for human consumption.
- Users may move, edit, or delete output files at any time. Never link wiki articles to files in `output/` or make the website depend on them.
- Preserve lasting project knowledge separately in the appropriate wiki articles under the normal readiness, maintenance, and concurrency rules. A human-readable report does not replace durable project memory. Template-maintenance deliverables must leave project wiki articles and logs untouched.
- Leave deliverables for the user to manage unless asked otherwise. Contents are ignored by Git except `output/.gitkeep`, which includes the directory in new clones.

## Temporary User Handoffs

When the user asks you to review material in `temp/`, inspect the relevant files. Screenshots can show how current website changes look; proposals can inform future work.

- Preserve information valuable for future reference in the appropriate `wiki/articles/` pages. Keep proposals distinguishable from approved plans or decisions.
- If the original file is worth retaining, copy it into the appropriate `wiki/raw/` subdirectory: visual references into `inspiration/`, content and proposals into `content/`, and research sources into `research/`. Use a descriptive filename and avoid overwriting existing sources.
- Wiki articles must be self-contained or reference retained files in the wiki. Never link to files in `temp/` or depend on their continued availability. When citing a source file, cite its retained copy.
- Do not automatically archive everything in `temp/`. Retain what matters to the task and tell the user what you preserved and where.
- Leave temporary originals for the user to manage unless asked to delete them. Temporary contents are ignored by Git; only `temp/.gitkeep` is tracked to include the directory in new clones.
- Follow the existing setup readiness and wiki concurrency rules before writing project-specific wiki content. Material in `temp/` does not authorize running `/setup`.

## Agent Working Files And Review Skills

Use `wiki/temp/` for agent-generated working artifacts; top-level `temp/` is for human-provided handoffs. Neither location is durable wiki memory. Never link wiki articles to files in either temporary directory or depend on those files remaining available.

When the user requests `/self-review` or a second-agent review, follow `.agents/skills/self-review/SKILL.md`. Prepare a review brief and hand it to a separate reviewer when available, or provide a portable prompt for a manual handoff. The reviewer inspects changes and reports findings without editing project files.

For `/uiux-self-review`, follow `.agents/skills/uiux-self-review/SKILL.md` to review responsive behavior, touch and keyboard interactions, accessibility, design fidelity, and visual improvements. For both review skills, the requesting agent must explain the recommendations to the human user and ask which changes they want implemented. Wait for explicit approval of selected recommendations before applying feedback; the review request or earlier build authorization does not supply that approval. Keep suggestions distinguishable from approved decisions.

The requesting agent owns cleanup: after receiving and processing feedback, acting on approved recommendations or preserving useful information as appropriate, and no longer needing the artifacts, delete only that review's working files. The reviewer must not delete them. Leave incomplete reviews, including those awaiting a user decision, available for resumption. Template-maintenance reviews must not initialize or update project wiki articles or logs.

## Before Meaningful Work

Before doing meaningful website, content, design, research, or strategy work:

1. Read `wiki/articles/index.md`.
2. Read `wiki/articles/log.md`.
3. Read relevant wiki articles such as `project-brief.md`, `design-direction.md`, `content-inventory.md`, `technical-architecture.md`, `research.md`, `task-roadmap.md`, `decisions.md`, and `open-questions.md`.
4. Check `wiki/raw/` for new source material when the task involves content, design direction, or research, and inspect relevant `input/assets/` and `input/mockups/` files when working with user design inputs.
5. Follow the wiki modification-check workflow before editing `wiki/articles/`, and check `.agents/locks/` before editing `site/`.

## Project Readiness Preflight

Before doing meaningful website, content, design, research, wiki strategy, or site implementation work, verify whether the wiki has enough project-specific information to proceed.

Start by reading the starter project articles:

- `wiki/articles/project-brief.md`
- `wiki/articles/design-direction.md`
- `wiki/articles/content-inventory.md`
- `wiki/articles/technical-architecture.md`
- `wiki/articles/research.md`
- `wiki/articles/task-roadmap.md`
- `wiki/articles/open-questions.md`
- `wiki/articles/log.md`
- `wiki/articles/decisions.md`

Treat `/setup` as not completed when the wiki is still boilerplate or lacks the minimum project definition needed for real work. Signals include:

- `project-brief.md` does not identify the website type, owner or brand, industry or field, expert perspective for research and strategy, primary goal, target audience, and likely pages or sections.
- `technical-architecture.md` does not identify a chosen stack or deployment assumption.
- `task-roadmap.md` says project-specific setup has not been run.
- The key project articles still mostly contain placeholder lines such as `Placeholder:` or `To be defined during /setup`.
- `wiki/articles/log.md` does not contain a setup entry such as `| setup | Initialized project wiki`.

The wiki content is the primary readiness signal. A setup log entry is useful supporting evidence, but it is not enough if the core articles still lack real project details.

If `/setup` has not been completed, do not proceed with project-specific website, wiki, or research work. Tell the user that this template still needs `/setup` to initialize the project wiki, then ask whether they want to run `/setup` now.

If the wiki is partially initialized but lacks information needed for the current task, ask focused follow-up questions or offer to resume `/setup` to fill the missing fields before continuing.

Template-maintenance work is allowed before `/setup` when the user is explicitly improving the template itself, the setup workflow, or agent instructions.

## After Meaningful Work

After doing meaningful work:

1. Update affected wiki articles.
2. Add durable decisions to `wiki/articles/decisions.md`.
3. Update `wiki/articles/task-roadmap.md`.
4. Append a chronological entry to `wiki/articles/log.md`.
5. Update `wiki/articles/index.md` if wiki pages were created, renamed, removed, or meaningfully changed.

## Repo-Local `/setup`

When the user asks for `/setup`, or explicitly invokes the repo-local `setup` skill, read and follow `.agents/skills/setup/SKILL.md`.

The `/setup` workflow is an actual repo-local skill at `.agents/skills/setup/SKILL.md`. It should remain portable and checked into the repository. Do not install, create, or require global, system-wide, user-profile, or machine-level skills for this template.

## Wiki Maintenance Standards

Keep wiki articles concise, structured, and useful to future agents. Use markdown headings, bullet lists, cross-links, and dated entries where helpful.

When information comes from raw source files, mention the source file. When something is an agent inference, label it as an inference.

Do not let the wiki become a transcript. Synthesize important context, decisions, open questions, risks, and progress.

## Research Standards

Project-specific research is allowed only after `/setup` has initialized the project wiki, because research guidance depends on the website type, field, audience, goals, and expert lens captured during setup.

When the user asks research-related questions after setup:

1. Act as an expert in the relevant field documented in `project-brief.md`, including any specific expertise lens requested during `/setup`.
2. Support both user-provided source material from `wiki/raw/research/` and web/current research when appropriate.
3. Preserve only meaningful synthesized findings in `wiki/articles/research.md` when they may affect strategy, content, design, SEO, positioning, technical choices, or future decisions.
4. Do not blindly catalog search results. Summarize what matters, cite sources for web/current claims, label agent inference, and note confidence or uncertainty.
5. If it is unclear whether a finding is relevant or useful enough to keep, ask the user whether to file it in the wiki.

Use `wiki/raw/research/` for source material and `wiki/articles/research.md` for synthesized research memory. Use `wiki/raw/inspiration/` for visual and design references, even when those references are competitors or examples.

## Website Development Standards

All website implementation work goes inside `site/`.

Default to static HTML, CSS, and JavaScript that a simple static server can serve after the user uploads the public website files by FTP. The default site must not require an application server, database, server-side runtime, serverless functions, special routing rewrites, or a managed backend service. Keep navigation and asset paths compatible with ordinary static hosting.

Introduce a backend or backend-dependent architecture only when the user explicitly requests it or chooses it after you explain why a requested feature needs it. Experience level alone is not authorization. If a feature cannot work with static files alone, explain the limitation and available options, then ask which approach the user wants before adding infrastructure or external services. Do not present a visual-only feature as functional. A frontend framework or build tool does not automatically imply approval for a backend; static output remains the deployment target unless otherwise requested.

The following organization and implementation preferences can adapt to project needs; the requirement for explicit user direction before introducing a backend still applies:

- Do not assume Node.js, npm, or other development tools are installed. Do not run package installs or introduce a build pipeline by default. Prefer browser-ready libraries loaded through ordinary script and stylesheet tags. If tooling is needed, explain why and establish the user's preference before introducing it; an explicitly chosen stack can provide that authorization.
- Prefer downloading needed third-party libraries and serving them locally under `site/assets/vendor/` over relying on CDN URLs at runtime. Use official distribution sources, retain license notices, and record versions and sources in the initialized project's technical notes. Avoid unnecessary dependencies.
- Keep files organized within `site/`, for example `assets/css/`, `assets/js/`, `assets/images/`, `assets/video/`, and `assets/fonts/`. Create directories as needed rather than scaffolding unused structure.
- Prefer separate CSS and JavaScript files over embedding styles and scripts in HTML. Split JavaScript by meaningful feature or reusable component when helpful. Use deferred loading, on-demand loading, or selective preloading as appropriate; do not preload every file by default.
- For repeated structures such as portfolio projects, consider reusable rendering logic with content in separate `.js` files containing objects and arrays. Prefer ordinary script tags, with content loaded before the rendering code, when direct-file previews matter. Keep data under a single clear namespace. JSON remains an option when its loading requirements suit the project; do not add abstraction to pages that are simpler as HTML.
- Preserve accessibility, useful document structure, and discoverability when choosing what to render with JavaScript. Check direct-file compatibility rather than assuming it: modules, fetch requests, and other features may require HTTP.

### Functionality And Asset Notes

If the intended behavior of a feature is unclear, ask a focused question about what the user should be able to do and what should happen next. Continue independent work where possible. Do not invent consequential behavior or present a mockup, placeholder, or disconnected control as a completed working feature. Clearly explain what works, what is a demonstration, and what remains unresolved, including any needed backend or external service choices.

Keep concise provenance notes for retained third-party images, fonts, icons, and libraries when sources are known. Preserve supplied license notices, note known usage restrictions, and label uncertain permissions as unknown rather than assuming clearance. Offer practical suggestions or cautions and alternatives; missing provenance alone must not block setup or unrelated development or turn into a blanket licensing questionnaire. Do not present these notes as legal clearance.

### Deployment Help When Requested

Do not require hosting provider, domain, FTP, or deployment details during setup. Assume ordinary static hosting and defer those specifics until the user requests deployment help. Preserve volunteered constraints without turning them into an upfront hosting questionnaire.

When asked, gather only the details needed for the requested handoff. Explain which public files to upload, where the homepage lives, the relevant document-root location if known, and any actual hosting requirements. The default static site must work independently of `input/`, `output/`, `temp/`, and the wiki. Identify the public deployment files within `site/`; do not instruct users to upload private configuration or the entire repository. If a written handoff is requested, use `output/` unless another destination is specified. Explain transfer and verification steps in the user's preferred style; guidance does not authorize publishing or changing hosting settings.

### Responsive Design

Build sites to remain usable across mobile, tablet, and desktop displays, including widths between supplied mockups and changes in orientation. Follow the user's explicit responsive directions and mockups as closely as possible.

When responsive guidance is absent or incomplete, make small, proportionate adjustments to layout, spacing, typography, navigation, and media so content remains readable and controls usable. Preserve the intended design and content hierarchy; ordinary gap-filling does not require approval for each adjustment.

If supplied directions contradict one another or would cause layout or usability problems, explain the specific conflict and its visible effect in plain language, offer practical options, and ask for guidance before deciding the conflicting behavior. Continue independent work where possible rather than silently overriding an explicit requirement.

Verify representative narrow, medium, and wide viewports, plus intermediate widths where the layout changes, using available browser tools. Check for unintended horizontal overflow, clipped or overlapping content, unreadable text, distorted media, and unusable navigation or controls. Report what was checked and any limits; do not claim device testing that was not performed.

### Local Preview

When a site is ready for the user to test, offer to start a local preview server if the environment supports it. Explain that it provides a local browser preview and ask whether the user wants it started, unless they have already authorized it. Do not assume Node.js or npm is available or install a runtime just to preview the site; inspect available tools and use a suitable existing server.

Serve only `site/`, bind to the local loopback interface, and provide the working URL and how to stop the server. Check for an existing appropriate preview before starting another, track any process you start, and do not terminate unrelated processes. If no suitable server is available, explain practical preview options and any direct-file limitations in plain language. A preview server is a development convenience, not a production hosting requirement.

Prioritize clear content hierarchy, a strong first impression, mobile responsiveness, fast loading, accessible markup, maintainable structure, visual consistency, and realistic content usage.

When inspiration exists in `wiki/raw/inspiration/`, use it to inform layout, visual tone, typography, color, spacing, and interaction choices. When content exists in `wiki/raw/content/`, adapt it into website-ready copy instead of copying raw material verbatim unless that is clearly appropriate.

## User Collaboration

Assume users may not be developers. Explain technical choices in plain language, ask focused questions when needed, and handle implementation work directly.

During setup, ask about comfort with HTML, CSS, and JavaScript and preferred explanation style, then record concise preferences in the project brief's User Collaboration section. Future agents should read and use those preferences. For users requesting plain language, focus on visible behavior, user impact, choices, and tradeoffs rather than unsolicited code walkthroughs. For intermediate users, add useful technical context selectively. For experienced users who want technical explanations, provide relevant implementation detail and verification evidence.

Do not infer experience from a job title or treat experience as a fixed label. Follow explicit preferences over assumptions, adapt when the user requests a different level of detail, and use plain language when preferences are unknown. Communication style does not reduce implementation standards or change authorization and review-approval requirements.

Once the website type and industry are known, act as an expert in that domain as well as a wiki manager and website developer. Help make the website strategically better, not merely technically complete.

## Concurrency

Agents may work in parallel. Wiki articles use modification checks and merging; website development uses repo-local locks. Do not use global lock files or system-level coordination.

### Wiki Articles: Check, Reread, And Merge

Do not create hard locks for `wiki/articles/`, including during `/setup`.

1. When reading an article, record its last-modified time (preferably UTC with full available precision) alongside the content you read. A content hash is recommended as an additional check because timestamps can miss changes. If the file changes during the read, reread it to establish a consistent baseline.
2. Immediately before each write, compare the current last-modified time with that baseline, and compare the hash if recorded. Treat a newly created or deleted file as a change too; do not overwrite an unexpected new file or recreate a deleted one without reassessing.
3. If anything changed since your read, reread the current file and reevaluate how and where to fold in your information. Preserve other agents' contributions and resolve duplication or conflicting statements deliberately. Repeat the check against this new baseline before writing.
4. Prefer narrow, context-sensitive patches that fail if the expected text has changed. If a patch fails, reread and merge again; never force a stale replacement or write an old full-file snapshot over newer content.
5. Reread the result after writing to verify your intended change and preservation of existing contributions. If you detect interference, reconcile against the latest content instead of restoring your old version. Refresh your baseline for subsequent writes. Ask the user only when conflicting meaning or intent cannot be resolved from available context.

Apply this workflow to every article write, including `log.md`, `decisions.md`, `task-roadmap.md`, and `index.md`. For log entries, preserve all existing entries, avoid duplicates, and use a timestamp with timezone and an agent or task identifier to distinguish concurrent work. Fold the entry into chronological order using the latest file contents. Logs explain completed changes; they do not reserve files or replace per-file checks. Template-maintenance work must not initialize or update project wiki articles or logs.

Modification checks and context-sensitive patches reduce conflicts but do not provide an atomic transaction across files. Keep edits small and reconcile related wiki pages when concurrent work affects their consistency.

### Website Development: File Locks

Before editing `site/`:

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
