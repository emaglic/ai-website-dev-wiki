---
name: uiux-self-review
description: Hand off an independent UI and UX review of a website, covering responsive layouts, touch and keyboard interactions, accessibility, and visual improvements, then present recommendations for user selection before implementing changes.
---

# Independent UI And UX Review

Use a separate reviewer to evaluate the site's appearance and usability. Review both concrete defects and opportunities for improvement, clearly distinguishing the two. This portable repo-local workflow does not authorize running `/setup`, redesigning the site, or implementing feedback without human approval.

## Prepare The Handoff

Read the agent guide and relevant initialized project wiki, including design direction, audience, and user requirements. Apply project readiness rules. Creating or maintaining this template skill does not require initializing a website; actually reviewing a project requires a site to review.

Establish the requested pages, interactions, and design references. If unspecified, use the site areas affected by the current task; ask for scope if no target is clear. A UI/UX review may cover existing behavior even without a Git diff.

Create a unique `wiki/temp/uiux-self-review-YYYYMMDD-HHMMSS-agent-id/` directory for `brief.md`, `feedback.md`, and supporting screenshots. Record the site revision or current worktree state so drift can be identified. Include intended behavior, relevant requirements and mockups, target pages, and known preview instructions without suggesting the conclusions the reviewer should reach. Input mockups are mutable: identify the version reviewed or retain a snapshot in this working directory if necessary. Never link durable wiki articles to temporary inputs or review files.

Use an appropriate existing preview if available. If a server is needed, follow the agent guide's preview rules: ask before starting unless already authorized, use available tools without assuming Node/npm, and serve only `site/` on loopback. Do not install tools just to enable the review without agreement. If browser access is unavailable, scope the review to available screenshots and source inspection and clearly disclose the resulting limits.

Launch a fresh separate reviewer with the brief and repository access when supported, preferably without the author's conversation history. Pause edits to the reviewed scope. If separate-agent execution is unavailable, provide the brief path and a portable handoff prompt for another agent; leave the review pending rather than claiming an independent review occurred.

## Reviewer Instructions To Include In The Brief

The reviewer may inspect code, references, and the site and write only the designated feedback and supporting evidence in this review directory. No project edits, fixes, wiki updates, commits, deletion, or recursive delegation. Use non-destructive interactions; do not submit real forms, make purchases, or change external data. Report scope drift rather than silently reviewing different content.

Evaluate relevant user journeys and pages, including:

- Responsive behavior at narrow, medium, wide, and intermediate viewports, plus orientation changes where supported. Look for overflow, clipping, overlap, broken grids, unreadable text, and unsuitable image crops or proportions.
- Touch and pointer behavior: hover-only content or controls, first-tap behavior, menus, galleries, tooltips, and alternatives for devices without hover. Consider hybrid devices; screen width alone does not establish input capability.
- Keyboard use and visible focus, navigation and dismissal of overlays, focus order, control labels, contrast, touch targets, and motion preferences. Report observed accessibility problems without claiming a full compliance audit.
- Visual hierarchy, typography, spacing, consistency, navigation clarity, feedback, and relevant loading, empty, and error states. Offer specific improvements aligned with the audience, goals, and approved design rather than imposing personal taste.
- Fidelity to supplied mockups and responsive instructions. Identify conflicting directions and their user-visible consequences; ask for clarification instead of assuming permission to override them.

Use available browser tools to inspect actual rendering and interactions where possible, supported by source inspection. Distinguish viewport emulation from physical-device testing, and observed behavior from inference. Screenshots alone cannot verify interaction, keyboard, or touch behavior. State what could not be tested.

Ask for `feedback.md` containing stable finding identifiers and prioritized findings. Each finding should identify its category (defect, design suggestion, or requirement conflict), affected page/component and relevant source location, viewport/input conditions, reproduction steps or evidence, user impact, recommended change, and material tradeoffs. Reference screenshots when useful. Separate blockers from optional visual polish, and finish with coverage and verification limits. An honest report with no actionable findings is acceptable.

## Present Feedback, Obtain Approval, And Clean Up

The requesting agent owns the lifecycle, not the reviewer. Follow the feedback processing, user approval, and cleanup rules in [the code-review skill](../self-review/SKILL.md#requesting-agent-process-feedback-and-own-cleanup); reuse that lifecycle without launching an additional code review.

Validate and explain recommendations to the human user, then ask which identified changes they want implemented. Wait for explicit selection before applying any reviewer feedback. Invoking the review or an earlier build task is not approval. Preserve pending artifacts while waiting. Implement only approved changes, then verify relevant layouts and interactions; any new recommendations need approval too.

Preserve lasting project knowledge in appropriate wiki articles with accurate pending, approved, or declined status under normal concurrency rules. Do not promote suggestions into decisions. When the review is processed and its files are no longer needed, the requesting agent deletes only its own verified review directory. Leave interrupted or unresolved reviews available for resumption. Report approved changes, remaining findings, checks performed, and cleanup status. Never make durable wiki content depend on the temporary review files.
