---
name: setup
description: Initialize this website wiki template when the user requests /setup, including repo-local adaptation to their agent tool, or perform only agent adaptation when explicitly requested without reinitializing an existing project.
---

# Repo-Local `/setup` Workflow

Use this workflow when the user asks for `/setup`. This file is intentionally stored inside the repository so the template remains portable and self-contained. Do not create, install, or require global, system-wide, user-profile, or machine-level skills.

The goal of `/setup` is to initialize this generic website-wiki template for a specific website project. Run initialization only when the user explicitly asks for `/setup` or asks you to read and run this file for project initialization. If the user only asks to adapt an agent tool, perform only the agent adaptation section; do not run the project questionnaire or initialize/reset wiki articles. Maintaining the template itself never runs initialization.

## Role During Setup

Act as three roles at once:

- Wiki Manager: initialize and maintain the markdown wiki as project memory.
- Website Developer: choose and document a practical implementation approach for `site/`.
- Industry Expert: once the website type, field, and desired expertise lens are known, provide strategic guidance for that context.

Assume the user may not be a developer. Ask focused questions in plain language and handle the wiki updates yourself.

## Setup Principles

- Ask questions in small batches. Do not overwhelm the user.
- Keep the project generic until the user provides specifics.
- Default to static HTML, CSS, and JavaScript deployable by uploading public site files to ordinary static hosting via FTP. Add a backend only when explicitly requested or selected by the user after explaining a feature's requirements; coding experience alone does not authorize infrastructure.
- Do not assume Node.js/npm is available or introduce package installs by default. Follow the agent guide's website standards for local libraries, organized assets, separate CSS/JS, and reusable rendering with separate JavaScript content objects where helpful. These are defaults that can adapt to project needs.
- Treat `wiki/raw/` as source-of-truth input. Do not modify raw files unless explicitly asked.
- Treat `input/` as a mutable user design workspace. Follow the agent guide's copy-and-retain rules; never link project wiki articles to input files.
- Label inferences clearly when writing wiki articles.
- Use the agent guide's modification-check, reread, and merge workflow for every wiki article write. Use `.agents/locks/` only for work in `site/`.

## Initial Checks

Before asking project questions:

1. Read the authoritative `AGENTS.md`, even if you arrived through a tool-specific entry file.
2. Read `wiki/articles/index.md`.
3. Read `wiki/articles/log.md`.
4. Inspect `wiki/raw/inspiration/`, `wiki/raw/content/`, and `wiki/raw/research/` for existing source files, and `input/assets/` and `input/mockups/` for current user design inputs.
5. Record last-modified times when reading wiki articles, preferably with content hashes, and follow the agent guide's concurrency workflow immediately before and after each write. Do not create wiki locks.

## Agent Tool Adaptation

For `/setup`, complete this step before the project questionnaire. For an explicit request to add or switch agent tools, run this section alone and preserve the existing project wiki. Adapting a tool is independent of project initialization.

1. Identify the actual application and, when available, its version from reliable session context. Do not infer it from a model name, API provider, or the presence of `CLAUDE.md`/`GEMINI.md`; all clones can contain those files. If unclear, ask which tool the user uses, with examples such as Codex, Claude Code, Gemini CLI, or another editor/chat application. A project can support several tools at once.
2. Inspect existing repository configuration before writing. Keep `AGENTS.md` and `.agents/skills/` authoritative. Preserve user settings and unrelated files; do not overwrite a conflicting command or skill. Reuse adapters that already point at the correct shared workflow. Ask about actual conflicts instead of replacing custom behavior.
3. Check documented discovery behavior for the tool/version, using official documentation when verification is needed. Current starting points:

   | Tool | Repository instructions | Shared workflow access |
   | --- | --- | --- |
   | Codex | `AGENTS.md` | `.agents/skills/` is a native discovery location; avoid redundant adapters. |
   | Claude Code | `CLAUDE.md` imports `@AGENTS.md` | Where needed, add thin skills under `.claude/skills/<name>/SKILL.md` pointing to the canonical workflow. |
   | Gemini CLI | `GEMINI.md` directs the agent to `AGENTS.md` | Versions supporting the `.agents/skills/` alias need no duplicate skills; verify discovery. |
   | Other tools | A documented repo-local instruction entry, if supported | Use a documented local adapter or explicit file-based instructions. Never invent configuration or assume native slash commands. |

4. When native registration needs an adapter, create only the necessary small files. For a Claude Code skill wrapper, use YAML frontmatter with the canonical skill's `name` and an accurate `description`, followed by an instruction such as: "Read and follow `.agents/skills/self-review/SKILL.md` from the repository root. That file is authoritative; do not substitute this adapter for its workflow." Generate wrappers for the three shared skills as needed, changing the target path and description for each. Do not copy workflow bodies, use symlinks that require special platform permissions, change global settings, install tools, or relax execution permissions. Native invocation is a convenience, not a prerequisite.
5. Verify generated files and target paths and, where supported, check actual skill discovery. If a reload or restart is needed, explain it. Do not claim runtime compatibility based only on file creation. If the environment cannot register skills or access the repository, explain what the user must open or attach and provide the explicit instruction: "Read AGENTS.md, then read and follow .agents/skills/<name>/SKILL.md." Do not claim adaptation can grant missing capabilities.
6. Report detected tools, files added or reused, invocation instructions, and any unverified behavior. During project initialization, record useful tool and invocation notes in `technical-architecture.md` with normal concurrency checks. For adaptation alone, leave wiki articles and logs untouched unless the user asks to update them. Later tool changes must not erase existing adapters or reset the project.

Official discovery references: [Codex skills](https://learn.chatgpt.com/docs/build-skills), [Claude Code skills](https://code.claude.com/docs/en/skills), [Claude Code shared instructions](https://code.claude.com/docs/en/memory), [Gemini CLI context](https://geminicli.com/docs/cli/gemini-md/), and [Gemini CLI skills](https://geminicli.com/docs/cli/tutorials/skills-getting-started/). Verify these rather than assuming other products from the same provider behave identically.

## Setup Questionnaire

Ask these questions in batches of 3 to 5. Adapt wording to the user, but preserve the intent.

### Experience And Communication

Ask early, alongside the first project questions, unless the user has already provided this information:

"How comfortable are you with HTML, CSS, and JavaScript: new to code, comfortable with some edits, or experienced? Would you prefer explanations focused on what visitors see and can do, a mix of plain language and technical detail, or detailed code explanations?"

Experience and explanation preference can differ. If useful, ask one focused follow-up about differences between HTML/CSS and JavaScript comfort or whether the user wants to learn while building. Do not turn this into a technical quiz, infer ability from a job title, or require an answer before continuing. If unanswered, use plain language and mark the preference as unspecified rather than inventing an experience level.

Use the response throughout setup and future collaboration:

- For users new to code or requesting plain language, explain visible behavior, user impact, options, and tradeoffs. Avoid unsolicited walkthroughs of variables, functions, or implementation internals.
- For intermediate users or a mixed preference, lead with behavior and add selective technical detail relevant to their question or decision.
- For experienced users requesting technical detail, include relevant implementation choices, code structure, constraints, and verification evidence without explaining basics unnecessarily.

Explicit communication preferences take priority over assumed experience. Users can request more or less detail at any time. These preferences affect communication, not implementation quality, architecture authorization, or approval requirements. During initialization, synthesize the preference in a **User Collaboration** section of `project-brief.md` so every provider's agent can use it; do not store a questionnaire transcript.

### Project Identity

1. What kind of website are we building?
   - Portfolio, business website, blog, ecommerce, landing page, personal site, etc.
2. Who is the website for?
   - Person, brand, company, studio, organization, product, or project.
3. What industry or creative field does it belong to?
   - Design, art direction, technology, healthcare, music, consulting, etc.
4. What expert perspective should future agents use when giving strategic or research guidance?
   - Examples: luxury ecommerce strategist, local service business marketer, gallery curator, healthcare content strategist, SaaS growth advisor, nonprofit communications lead, etc.

### Goals And Audience

5. What is the primary goal of the website?
   - Get clients, showcase work, sell products, publish writing, build credibility, collect leads, etc.
6. Who is the intended audience?
   - Recruiters, clients, collaborators, customers, fans, investors, etc.
7. What would make the website successful?
   - Concrete outcomes, user actions, business results, quality standards, or launch criteria.

### Structure And Content

8. What pages or sections are likely needed?
   - Home, About, Work, Case Studies, Services, Contact, Blog, Shop, Resume, etc.
9. What raw content, inspiration, or research has already been provided in `wiki/raw/`?
10. Is any content missing, sensitive, outdated, or not ready to publish?

### Design Direction

11. What visual tone should the site have?
    - Minimal, editorial, playful, premium, technical, warm, bold, refined, experimental, etc.
12. Are there inspiration sources, references, competitors, or examples to consider?
13. Are there brand constraints such as logo, colors, typography, imagery, voice, or existing materials?

### Technical Approach

14. What technical approach should we use?
    - Explain the default in plain language: static HTML/CSS/JS that can be uploaded via FTP, with no Node.js/npm, build step, or backend required. Ask whether the user has a different preference rather than requiring a nontechnical user to choose a framework.
    - React, Vue, Svelte, or another app framework
    - Static site generator
    - Component framework
    - Other
    - Discuss a backend only if the user requests one or a requested feature needs capabilities beyond static files. Explain implications and obtain the user's choice before adopting it; a framework preference does not itself authorize a backend.
15. Are there constraints?
    - Must be easy to FTP
    - No database
    - Mobile-first
    - Must load fast
    - Must be easy to edit later
    - Must match an existing brand

Do not ask for a hosting provider, domain, FTP details, credentials, or deployment destination during initialization. Record the static/FTP assumption and "deployment details deferred until requested." Preserve any details the user volunteers, without requiring follow-up hosting questions. Unknown hosting details do not block setup or static website work. Discuss deployment specifics later when the user requests help; clarify feature requirements now only if they affect the architecture the user wants.

## Wiki Initialization

After the setup conversation, update these files:

- `wiki/articles/project-brief.md`
- `wiki/articles/design-direction.md`
- `wiki/articles/content-inventory.md`
- `wiki/articles/technical-architecture.md`
- `wiki/articles/research.md`
- `wiki/articles/task-roadmap.md`
- `wiki/articles/open-questions.md`
- `wiki/articles/decisions.md`
- `wiki/articles/index.md`
- `wiki/articles/log.md`

Use concise synthesized notes, not a transcript. Link related wiki pages where useful.

## Completion Signals

When setup is complete, remove starter placeholder text from the core project fields and leave a clear project-ready signal:

- `project-brief.md` identifies the website type, owner or brand, industry or field, expert perspective for research and strategy, primary goal, target audience, likely pages or sections, success criteria, and constraints.
- `technical-architecture.md` identifies the chosen stack and hosting or deployment assumption, even when the answer is "static HTML/CSS/JS" and "deployment not yet chosen."
- `task-roadmap.md` no longer says project-specific setup has not been run.
- `open-questions.md` contains only unresolved follow-ups, not the full starter questionnaire.
- `log.md` contains `## YYYY-MM-DD | setup | Initialized project wiki`.

If the user cannot answer every setup question, record known answers, mark unknowns as open questions, and make clear whether the project is ready for initial website work or still blocked by missing essentials.

## Article-Specific Guidance

### `project-brief.md`

Record the central project definition:

- User collaboration: self-described HTML/CSS/JavaScript comfort, preferred explanation style, and any useful differences by topic or interest in learning; keep unspecified answers explicitly unknown
- Website type
- Website owner or brand
- Industry or field
- Expert perspective for research and strategy
- Primary goal
- Target audience
- Key pages or sections
- Success criteria
- Constraints

### `design-direction.md`

Summarize visual strategy:

- Desired visual tone
- Inspiration sources
- Color direction
- Typography direction
- Layout principles
- Interaction style
- Accessibility considerations

### `content-inventory.md`

Summarize content status:

- Raw content sources
- Extracted facts
- Website-ready copy ideas
- Missing content
- Content risks or sensitivities

Mention source files from `wiki/raw/content/`, `wiki/raw/inspiration/`, and `wiki/raw/research/` when applicable.

### `research.md`

Initialize the research memory:

- Research scope and expert lens
- User-provided research sources from `wiki/raw/research/`
- Meaningful findings that already affect strategy, content, design, SEO, positioning, technical choices, or future decisions
- Open research questions

Do not blindly catalog everything discovered during web research. Preserve synthesized findings only when they are meaningful to the project. Cite sources for web/current claims, label agent inference, note confidence or uncertainty, and ask the user before filing findings whose relevance is unclear.

### `technical-architecture.md`

Document implementation decisions:

- Chosen stack
- Agent tools, repo-local adapters, workflow invocation, and any discovery limitations established during setup
- Hosting/deployment assumptions only; leave provider and upload details deferred until the user requests deployment help
- Static/FTP deployment as the default, or the user's explicit choice of a backend with its requirements and rationale; distinguish public upload files from source or private configuration
- Directory conventions
- Asset strategy
- Browser/device support
- Build steps, if any
- Preview approach and available tools, without assuming Node.js/npm; offer to start a local server when the site is ready to test, asking first unless already authorized
- Local third-party library sources, versions, and licenses when used
- Content organization and reusable rendering approach where helpful; separate JavaScript objects/arrays can avoid JSON fetching for direct-file previews

Unless the user explicitly chooses otherwise, plan for public static files that can be uploaded via FTP and served without backend infrastructure. A local preview server does not change that production assumption.

### `task-roadmap.md`

Initialize:

- **Resume Here**: current task and status, last meaningful activity, unfinished work or verification, pending decisions/input, and the next concrete action; follow the agent guide's automatic logging and resumption rules
- Current status
- Next tasks
- Backlog
- Completed work
- Blocked items

### `open-questions.md`

Track unresolved:

- Project strategy questions
- Content questions
- Design questions
- Technical questions
- Deployment questions

### `decisions.md`

Record durable setup decisions with:

- Date
- Decision
- Rationale
- Alternatives considered
- Impact

### `index.md`

Update page summaries if the meaning or contents of starter pages changed during setup. Add any new wiki pages.

### `log.md`

Append a setup entry using this format:

```markdown
## YYYY-MM-DD | setup | Initialized project wiki

- Summary:
- Files changed:
- Decisions:
- Follow-ups:
```

## Post-Setup Guidance

After `/setup` is complete:

1. Verify the final wiki content against the latest concurrent contributions. If site work was also authorized, release any site locks you created after completing that work.
2. Tell the user which wiki files were initialized.
3. Explain the recommended next development step.
4. Explain that future project work automatically updates the log and roadmap, and that the user can ask "Where did we leave off?" in a later session. Continue from the initialized wiki and authoritative `AGENTS.md`; tool-specific entry files only route to that guide.

The setup skill may remain in the repository for future reference, but ongoing agents should rely primarily on the initialized wiki.
