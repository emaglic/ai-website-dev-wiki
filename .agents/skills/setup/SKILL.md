---
name: setup
description: Use when the user asks to run /setup or initialize this website wiki template for a real website project. This repo-local workflow gathers project details, initializes the wiki, and prepares the site roadmap.
---

# Repo-Local `/setup` Workflow

Use this workflow when the user asks for `/setup`. This file is intentionally stored inside the repository so the template remains portable and self-contained. Do not create, install, or require global, system-wide, user-profile, or machine-level skills.

The goal of `/setup` is to initialize this generic website-wiki template for a specific website project. Do not run this workflow unless the user explicitly asks for `/setup`.

## Role During Setup

Act as three roles at once:

- Wiki Manager: initialize and maintain the markdown wiki as project memory.
- Website Developer: choose and document a practical implementation approach for `site/`.
- Industry Expert: once the website type, field, and desired expertise lens are known, provide strategic guidance for that context.

Assume the user may not be a developer. Ask focused questions in plain language and handle the wiki updates yourself.

## Setup Principles

- Ask questions in small batches. Do not overwhelm the user.
- Keep the project generic until the user provides specifics.
- Prefer static HTML, CSS, and JavaScript when the user wants FTP-friendly deployment and has no special technical requirements.
- Treat `wiki/raw/` as source-of-truth input. Do not modify raw files unless explicitly asked.
- Label inferences clearly when writing wiki articles.
- Coordinate with `.agents/locks/` before editing `wiki/articles/` or `site/`.

## Initial Checks

Before asking project questions:

1. Read `AGENTS.md` or the relevant agent guide.
2. Read `wiki/articles/index.md`.
3. Read `wiki/articles/log.md`.
4. Inspect `wiki/raw/inspiration/`, `wiki/raw/content/`, and `wiki/raw/research/` for existing source files.
5. Check `.agents/locks/` for overlapping locks on `wiki/articles/`.
6. Create a narrow lock for the wiki articles you will update.

## Setup Questionnaire

Ask these questions in batches of 3 to 5. Adapt wording to the user, but preserve the intent.

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
    - Static HTML/CSS/JS
    - React, Vue, Svelte, or another app framework
    - Static site generator
    - Component framework
    - Other
15. Are there constraints?
    - Must be easy to FTP
    - No database
    - Mobile-first
    - Must load fast
    - Must be easy to edit later
    - Must match an existing brand
16. How should the finished website be hosted or deployed, if known?

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
- Hosting/deployment assumptions
- Directory conventions
- Asset strategy
- Browser/device support
- Build steps, if any

If the user wants FTP-friendly deployment and no special technical requirements exist, recommend simple static HTML, CSS, and JavaScript.

### `task-roadmap.md`

Initialize:

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

1. Remove any setup lock files you created.
2. Tell the user which wiki files were initialized.
3. Explain the recommended next development step.
4. Continue future work from the initialized wiki and the durable operating rules in `AGENTS.md` or `CLAUDE.md`.

The setup skill may remain in the repository for future reference, but ongoing agents should rely primarily on the initialized wiki.
