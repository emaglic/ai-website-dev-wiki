# Repo-Local `/setup` Workflow

Use this workflow when the user asks for `/setup`. This file is intentionally stored inside the repository so the template remains portable and self-contained. Do not create, install, or require global, system-wide, user-profile, or machine-level skills.

The goal of `/setup` is to initialize this generic website-wiki template for a specific website project. Do not run this workflow unless the user explicitly asks for `/setup`.

## Role During Setup

Act as three roles at once:

- Wiki Manager: initialize and maintain the markdown wiki as project memory.
- Website Developer: choose and document a practical implementation approach for `site/`.
- Industry Expert: once the website type and field are known, provide strategic guidance for that context.

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
4. Inspect `wiki/raw/inspiration/` and `wiki/raw/content/` for existing source files.
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

### Goals And Audience

4. What is the primary goal of the website?
   - Get clients, showcase work, sell products, publish writing, build credibility, collect leads, etc.
5. Who is the intended audience?
   - Recruiters, clients, collaborators, customers, fans, investors, etc.
6. What would make the website successful?
   - Concrete outcomes, user actions, business results, quality standards, or launch criteria.

### Structure And Content

7. What pages or sections are likely needed?
   - Home, About, Work, Case Studies, Services, Contact, Blog, Shop, Resume, etc.
8. What raw content or inspiration has already been provided in `wiki/raw/`?
9. Is any content missing, sensitive, outdated, or not ready to publish?

### Design Direction

10. What visual tone should the site have?
    - Minimal, editorial, playful, premium, technical, warm, bold, refined, experimental, etc.
11. Are there inspiration sources, references, competitors, or examples to consider?
12. Are there brand constraints such as logo, colors, typography, imagery, voice, or existing materials?

### Technical Approach

13. What technical approach should we use?
    - Static HTML/CSS/JS
    - React, Vue, Svelte, or another app framework
    - Static site generator
    - Component framework
    - Other
14. Are there constraints?
    - Must be easy to FTP
    - No database
    - Mobile-first
    - Must load fast
    - Must be easy to edit later
    - Must match an existing brand
15. How should the finished website be hosted or deployed, if known?

## Wiki Initialization

After the setup conversation, update these files:

- `wiki/articles/project-brief.md`
- `wiki/articles/design-direction.md`
- `wiki/articles/content-inventory.md`
- `wiki/articles/technical-architecture.md`
- `wiki/articles/task-roadmap.md`
- `wiki/articles/open-questions.md`
- `wiki/articles/decisions.md`
- `wiki/articles/index.md`
- `wiki/articles/log.md`

Use concise synthesized notes, not a transcript. Link related wiki pages where useful.

## Article-Specific Guidance

### `project-brief.md`

Record the central project definition:

- Website type
- Website owner or brand
- Industry or field
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

Mention source files from `wiki/raw/content/` and `wiki/raw/inspiration/` when applicable.

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

