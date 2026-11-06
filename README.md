# AI Website Dev Wiki

Turn your ideas, mockups, and content into a website with an AI development partner—and give that partner a place to remember how the project fits together.

AI Website Dev Wiki is a reusable template for AI-assisted web development, from the first project brief through design, implementation, review, and deployment guidance. It brings your website files, design inputs, and project knowledge into one organized repository, with instructions that help agents work consistently across sessions and tools.

You can start with no coding experience, bring years of web development experience, or fall anywhere in between. Describe what you want to build, share the materials you have, and let the agent help turn those into a practical plan and working website. The default approach uses static HTML, CSS, and JavaScript, so getting started does not require Node.js, npm, or backend infrastructure.

## What This Template Is For

Use this template to create a portfolio, business website, landing page, or another web project with AI assistance. Each project starts from its own copy: run `/setup`, answer a few batches of questions, and the agent builds a shared understanding of your goals before implementation begins.

**For designers and people new to development**, it provides a way to work from familiar materials: mockups, images, written content, and descriptions of how the site should look and behave. Agents explain choices in plain language, handle implementation, and ask for direction when requirements are unclear. You do not need to learn a framework just to get your ideas onto a page.

**For experienced developers**, it provides a reusable foundation for organizing AI work: durable requirements and decisions, a task roadmap, concurrency rules, and independent code and UI/UX review workflows. You can request technical explanations and choose a more complex architecture when your project calls for it.

The template helps you:

- **Keep momentum between sessions.** Preserve important context so the next agent can pick up the work without making you repeat the entire brief.
- **Build from your own design direction.** Supply assets and mockups, then have agents implement and adapt them across screen sizes.
- **Get another perspective.** Request independent code or UI/UX feedback, understand the recommendations, and choose which changes to implement.
- **Keep the project organized.** Separate website development, evolving design inputs, temporary handoffs, and requested reports or plans.
- **Keep your options open.** Use shared instructions with different agent tools and providers, adapting repository-local integration where needed.

### What Is An LLM Wiki?

An LLM wiki is a collection of readable Markdown documents that an AI agent maintains as project memory. Here, those documents live in `wiki/articles/` and capture the website's goals, audience, design direction, content status, technical choices, research, decisions, and remaining work.

Think of it as a project notebook that travels with the code. A chat conversation can become long, lose context, or end entirely; the wiki keeps useful knowledge in files that you and future agents can inspect. Agents are instructed to read the relevant pages before project work and update them as the project evolves.

For example, if you decide that project images should open in a gallery, mobile navigation should use a particular pattern, and the site should remain easy to upload by FTP, those choices can be recorded alongside their reasons. A later session can read that context before making changes instead of guessing or asking you to explain everything again.

The wiki stores concise, lasting knowledge rather than a transcript of every message. It does not give an agent automatic memory or guarantee that it will make the right decision; it gives agents an explicit, shared reference to consult. You stay in control of the direction while the project becomes easier to continue, review, and hand off.

## Quick Start: Your First Project

1. Create your own project repository from this template, then clone or download it to your computer. Keep each website project in its own copy.
2. Open that project folder in your preferred AI coding tool and give the agent access to its files. You do not need Node.js or npm for the default static website workflow.
3. Optionally add any materials you already have: website assets in `input/assets/`, design mockups in `input/mockups/`, and lasting copy, references, or research in the appropriate `wiki/raw/` folders. You can add more later; none of this is required to start.
4. Ask the agent to initialize the project wiki with `/setup`. If your tool does not recognize that command, paste:

   ```text
   Read AGENTS.md, then read and run .agents/skills/setup/SKILL.md to initialize this website project.
   ```

5. Answer the agent's questions in small batches. It will adapt to your agent tool, learn what you are building and how you prefer explanations, then write the project wiki. You can say "I'm not sure" rather than inventing an answer.
6. Review the agent's summary, correct anything it misunderstood, and ask it to start a specific piece of the website. Setup prepares the project memory and roadmap; the website is built afterward in `site/`.

### Example Setup Conversation

This abbreviated example shows the kind of exchange to expect; the agent adapts the questions to your project.

> **You:** /setup
>
> **Agent:** What kind of website are we building, and who is it for? How comfortable are you with HTML, CSS, and JavaScript, and how would you like me to explain things?
>
> **You:** A portfolio for my graphic design work. I don't write code, so explain what visitors will see and do. I want potential clients to browse my projects and contact me.
>
> **Agent:** What pages or sections do you want? Do you have copy, images, or mockups, and what visual direction should I follow?
>
> **You:** Home, Work, About, and Contact. I've added a logo and project images to input/assets/ and a homepage mockup to input/mockups/. Keep the design minimal and adapt it for mobile where I haven't provided a mockup.
>
> **Agent:** I'll plan a static site you can upload later without a backend. What should visitors be able to do on Contact—for example, open an email link? I'll also ask about any missing content and constraints before finishing the wiki.
>
> **You:** An email link is fine. I still need to write the About text.
>
> **Agent:** The wiki is initialized with the project brief, design direction, content inventory, technical plan, and roadmap. The About copy is noted as missing. No hosting details are needed yet. The first implementation task is the homepage.
>
> **You:** Build the homepage using my mockup and assets.

You can keep working with the same agent or start another session in the same project folder; the next agent should read `AGENTS.md` and the wiki before continuing. When a site is ready to test, the agent can offer a local preview. You can request `/self-review` or `/uiux-self-review` later and choose which recommendations to implement.

For more detail, see [Using Different AI Agents](#using-different-ai-agents) and [Getting Started With `/setup`](#getting-started-with-setup).

## Project Structure

```text
.
├── .agents/
│   ├── locks/              # Temporary coordination locks for site/ work
│   └── skills/             # Repo-local setup, code review, and UI/UX review workflows
├── site/                   # Website implementation files
├── input/                  # Mutable user design workspace (contents ignored by Git)
│   ├── assets/             # Assets to copy into site/ when used
│   └── mockups/            # Design mockups, including exported Figma images
├── output/                 # Requested human-readable deliverables, not site development
├── temp/                   # Disposable user handoffs (contents ignored by Git)
├── wiki/
│   ├── articles/           # LLM-managed project wiki
│   ├── temp/               # Disposable agent working files (ignored by Git)
│   └── raw/
│       ├── content/        # User-provided raw content
│       ├── inspiration/    # Visual references, screenshots, palettes, examples
│       └── research/       # Market, competitor, audience, SEO, and industry sources
├── AGENTS.md               # Operating instructions for AI agents
├── CLAUDE.md               # Claude adapter importing the shared instructions
├── GEMINI.md               # Gemini adapter directing agents to shared instructions
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

## Design Inputs

Use `input/assets/` for images, logos, fonts, and other assets intended for the website. Use `input/mockups/` for design mockups, such as JPG or PNG exports from Figma. This is your evolving design workspace: you can add, replace, edit, or delete files as the project develops.

Agents copy assets into the appropriate location under `site/` before using them. Website code references those copies, leaving your working originals intact unless you request otherwise. If a mockup version needs to become a lasting reference, the agent copies it into `wiki/raw/inspiration/`. Wiki articles reference retained copies and never link to files in `input/`.

All working contents of `input/` are ignored by Git; only `input/assets/.gitkeep` and `input/mockups/.gitkeep` are included in the template. The website and durable wiki must remain usable if you delete the inputs. Use top-level `temp/` for one-off handoffs instead.

## Human-Requested Deliverables

The top-level `output/` directory holds files you specifically ask the agent to create for your own consumption, such as project reports or human-readable implementation plans. You can move, edit, or delete these files whenever you like. If you specify a different destination, the agent uses that instead.

All website development happens in `site/`. Website code, styles, scripts, assets, configuration, build files, and other development files belong there. `output/` is not a place to develop or build the website. Internal agent working files belong in `wiki/temp/`.

Wiki articles never link to files in `output/`, and the website must not depend on them. Agents preserve lasting project knowledge separately in the wiki. Contents are ignored by Git except `output/.gitkeep`, so the directory ships with the template.

## Temporary Handoffs

Use the top-level `temp/` directory to give the agent temporary material, such as screenshots of the current website or draft proposals for future work. Ask the agent to review the relevant files and fold useful information into the wiki.

You can delete files from `temp/` whenever you like. Agents preserve valuable information in `wiki/articles/` and copy original files worth retaining into the appropriate `wiki/raw/` subdirectory. Proposals remain proposals until approved. Wiki references point to retained copies, never to temporary files.

The agent reports what it preserved and leaves temporary originals for you to manage unless you ask it to delete them. Contents of `temp/` are ignored by Git; a tracked `.gitkeep` ensures the directory exists in new clones. If you delete the directory itself, you can recreate it whenever needed.

## Independent Code Review With `/self-review`

Ask the agent to run `/self-review` to prepare a review brief and hand your changes to a separate agent for an independent code review. The repo-local workflow lives in `.agents/skills/self-review/SKILL.md`. If separate-agent execution is unavailable, the agent provides a prompt you can hand to another agent yourself.

Review briefs and feedback live in a unique directory under `wiki/temp/`, separate from human handoffs in top-level `temp/`. The reviewer reports findings without changing project files. The requesting agent explains recommendations and asks which changes you want implemented. It waits for your approval before applying reviewer feedback, then processes your selected changes and preserves useful information as appropriate. It deletes its review files once they are no longer needed. Incomplete reviews, including those awaiting your decision, remain available for resumption.

Contents of `wiki/temp/` are ignored by Git except `.gitkeep`. Durable wiki articles must never link to these working files. Reviewing the template itself does not initialize or update project wiki articles or logs.

## UI And UX Review With `/uiux-self-review`

Ask for `/uiux-self-review` to get a separate agent's assessment of responsive layouts, touch alternatives to hover, keyboard usability, accessibility, and visual design. It follows your mockups and design goals, distinguishing concrete problems from optional improvements. The workflow lives in `.agents/skills/uiux-self-review/SKILL.md` and supports manual handoff when separate-agent tools are unavailable.

As with `/self-review`, recommendations are explained to you first, and you choose which changes to approve before implementation. Review files stay under `wiki/temp/` until processed and no longer needed. The agent reports what it actually inspected; screenshots or viewport emulation are not presented as physical-device testing.

## Using Different AI Agents

There is one shared template for all providers. `AGENTS.md` contains the authoritative rules, and `.agents/skills/` contains the shared workflows. `CLAUDE.md` and `GEMINI.md` are small entry files that route agents to the same rules. They do not contain separate versions of project guidance.

During `/setup`, the agent identifies the application you are using, asks if it cannot tell, and adds only the repository-local adapters that application needs. Codex and supported Gemini CLI versions can discover `.agents/skills/`; Claude Code can use thin wrappers in `.claude/skills/`. Discovery and command syntax depend on the application and version. See the official [Codex](https://learn.chatgpt.com/docs/build-skills), [Claude Code](https://code.claude.com/docs/en/skills), and [Gemini CLI](https://geminicli.com/docs/cli/tutorials/skills-getting-started/) skill documentation.

If a command is not recognized, give the agent this instruction instead:

```text
Read AGENTS.md, then read and run .agents/skills/setup/SKILL.md to initialize this website project.
```

For reviews, use the same pattern with `.agents/skills/self-review/SKILL.md` or `.agents/skills/uiux-self-review/SKILL.md`. Your agent needs access to the repository; a chat application without file access needs you to provide the relevant files. Automatic discovery, browser inspection, and launching reviewers are not available in every tool. Review workflows include manual handoff as a fallback.

You can use more than one agent tool or switch later. Ask the agent to follow only the **Agent Tool Adaptation** section of `.agents/skills/setup/SKILL.md`, without initializing the wiki. It preserves project knowledge and existing adapters. No global installation or provider account configuration is required by the template; your chosen agent application still needs its own normal setup.

## Getting Started With `/setup`

When you are ready to turn this generic template into a real website project, ask your AI agent to run:

```text
/setup
```

The repo-local setup workflow lives at:

```text
.agents/skills/setup/SKILL.md
```

Native invocation varies by application: a supported interface may expose `/setup`, `$setup`, or a skill picker. If it does not, use the explicit file-based instruction above. Setup adapts repository-local workflow access to your tool before gathering project details.

During `/setup`, the agent will ask focused questions about:

- your comfort with HTML, CSS, and JavaScript and how you prefer changes and questions to be explained
- the kind of website you are building
- who or what the site is for
- the target audience and primary goal
- needed pages or sections
- available content and inspiration
- available research sources and the expert perspective agents should use
- visual direction and brand constraints
- preferred technical approach and constraints

After that, the agent initializes the wiki with project-specific strategy, content notes, design direction, technical choices, open questions, and a roadmap.

Your communication preferences are saved in the project brief so future agents can tailor explanations: visible behavior and plain language, a mix of practical and technical detail, or deeper code discussion. You can change your preference at any time. Coding experience is not required, and an experienced developer can still prefer concise, nontechnical explanations.

You do not need to choose a host or provide domain or FTP details during setup. The agent assumes ordinary static hosting and leaves deployment specifics until you request help.

Do not personalize this template for a specific website before running `/setup`. If an agent sees that the wiki is still mostly boilerplate or lacks the basic project definition needed for the task, it should pause project-specific work and ask whether you want to run `/setup` first.

## Building The Website

Website implementation belongs in `site/`.

The default is a static website built with HTML, CSS, and JavaScript. You can upload the public website files by FTP to ordinary static hosting without setting up an application server, database, serverless functions, or other backend infrastructure.

If you want a backend, the agent can build a more complex architecture when you explicitly request it. If a feature needs more than static files can provide, the agent explains the limitation and options and asks which approach you want before adding infrastructure or external services. Being an experienced developer or choosing a frontend framework does not automatically opt you into a backend.

You do not need Node.js or npm by default. Agents favor separate HTML, CSS, and JavaScript files, organized asset folders, and locally stored third-party libraries rather than runtime CDN links. Repeated layouts can use reusable JavaScript with content in separate JavaScript objects and arrays, without requiring a build step. These are practical defaults that can change to suit your project.

When the site is ready to test, the agent can offer to start a local preview server using tools already available, then provide a browser URL and instructions for stopping it. It asks before starting unless you have already authorized it. The server serves only `site/` locally. Some sites also work by opening HTML directly; agents explain when particular features require a server. No runtime is installed just to provide a preview without your agreement.

Agents build for mobile, tablet, and desktop displays, following your responsive directions and mockups closely. They make small adjustments where guidance is missing so the design remains usable between screen sizes. If your directions conflict or would create layout problems, the agent explains the issue and asks how you want to handle it. Agents check representative viewport sizes with available tools and report any testing limitations.

Future agents should choose the simplest technical architecture that satisfies the project goals and document that choice in `wiki/articles/technical-architecture.md`.

If a feature's behavior is unclear, agents ask what you want it to do. They distinguish working features from demonstrations and unfinished controls. They also keep useful asset source and license notes, offering cautions or alternatives when permissions are uncertain without blocking setup or unrelated work over missing provenance.

## Deployment Help

When you are ready, ask the agent for help uploading the site. It gathers the relevant hosting details then explains which public files to copy, where the homepage belongs, and how to check the deployed result. You do not upload the whole template: the default website works independently of the wiki and the temporary input/output directories. A requested written deployment guide goes in `output/` unless you choose another location. Providing instructions does not automatically publish the site or change your hosting configuration.

## Working With AI Agents

Agents should follow `AGENTS.md` before making meaningful changes. In short:

- read the wiki first
- check `wiki/raw/` for relevant source material
- check article modification times before each wiki write; reread and merge if changed
- coordinate edits to `site/` with `.agents/locks/`
- keep wiki updates concise and useful
- record durable decisions and progress
- keep website work inside `site/`

This makes the repository useful across multiple sessions, tools, and agents.

Agents can update wiki articles concurrently without hard locks. Each agent records a file's modification time when reading it and checks again immediately before writing. If the file changed, the agent rereads it and reconsiders how to fold in its information while preserving other contributions. Content hashes and context-sensitive patches add protection; agents verify the result after writing. The same rules apply to shared logs, which record completed work rather than reserve files. Website development in `site/` continues to use narrowly scoped locks. This coordination reduces conflicts but does not mechanically prevent simultaneous writes.

## Typical Workflow

1. Add any raw copy, notes, references, screenshots, or brand material to `wiki/raw/`.
2. Ask the agent to run `/setup`.
3. Review the initialized wiki and answer any open questions.
4. Build the website inside `site/`.
5. Keep the wiki updated as the project changes.

## Current State

This repository is currently a base template. Project-specific planning and website development should begin with `/setup`.
