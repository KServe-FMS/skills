# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

---

## Prime Directive

**Never produce final output until the human has reviewed and approved a written plan.**

Separate thinking from doing. Research prevents ignorant decisions. Planning prevents wrong decisions. Annotation injects human judgement. Execution becomes mechanical delivery of validated decisions.

---

## The Pipeline

```
Research → Plan → Annotate (1–6 rounds) → Task List → Execute → Feedback & Iterate
```

Every meaningful task follows this pipeline. The phases scale — a small task might compress Research + Plan into a single document; a large initiative might take six annotation rounds. But the sequence never changes, and no phase is skipped.

### Phase 1: Research

Deep investigation of the existing landscape before proposing anything. Always produce `research.md`. Document: what exists today, key components and relationships, existing conventions, constraints, gaps and risks. Flag uncertainties explicitly — never guess silently.

### Phase 2: Planning

Always produce `plan.md`. Every plan must include: Approach, Specifics, Scope, Artifacts, Considerations, and Impact. Do not execute yet.

### Phase 3: Annotation Cycle

The human annotates `plan.md` inline; the agent addresses every note and updates the plan. Repeat until the human approves. Do not execute yet.

### Phase 4: Task List

Add a granular checkbox task list (`- [ ]`) to `plan.md` broken into phases. Do not execute yet.

### Phase 5: Execution

Follow the plan exactly. Mark tasks `- [x]` as completed. Do not stop until all tasks are done unless a genuine blocker requires human input.

### Phase 6: Feedback & Iteration

Respond to short corrections immediately. Accept reverts gracefully — treat a narrowed scope as a fresh start, not a patch job.

---

## File Conventions

| File | Purpose | When Created |
|------|---------|--------------|
| `research.md` | Deep investigation findings | Phase 1 — Research |
| `plan.md` | Specification + task list + progress tracker | Phase 2 — Planning (updated through Phase 5) |

---

## Quality Standards

- **Follow existing conventions.** Match the patterns, terminology, and standards already in the repo
- **Don't over-engineer.** Deliver exactly what the plan specifies — no extra scope, abstraction, or complexity
- **Don't duplicate existing work.** Research should identify what already exists; reuse it
- **Be precise.** Specifics over generalities; named references over vague descriptions
- **Trim the fat.** No filler content — every element should earn its place
- Match the voice, tone, and terminology established in existing skill files
- Verify all cross-references between skill steps, waves, and mode-specific sections
- Keep structure scannable — use headings, spacing, and hierarchy intentionally

---

## Anti-Patterns

| Anti-Pattern | Why It Fails |
|--------------|--------------|
| Jumping straight to editing without research | Produces changes that ignore existing patterns and break surrounding steps |
| Verbal plans in chat instead of `plan.md` | Can't be annotated, reviewed holistically, or survive context compaction |
| Executing before the plan is approved | Wastes effort building on wrong assumptions |
| Skipping the annotation cycle | Misses human domain knowledge and business constraints |
| Adding scope during execution | Scope decisions belong in planning, not mid-execution |
| Surface-level research | Misses conventions, constraints, and integration points |

---

## Overview

KServe agent skills monorepo (`@kserve/skills`) — provides AI agent skills for KServe's BD team, installable via:

```bash
npx skills add @kserve/skills
npx skills add KServe-FMS/skills --skill company-research
```

No build, test, or lint commands exist. This is a pure Markdown/YAML skills repository; changes take effect immediately.

## Architecture

Each skill is a self-contained directory with a single `SKILL.md` file:

```
repo-root/
├── package.json          # npm package config (monorepo, files: ["*/"])
├── README.md
└── <skill-name>/
    └── SKILL.md          # YAML frontmatter + implementation instructions
```

### SKILL.md Structure

Every `SKILL.md` follows this pattern:

1. **YAML frontmatter** — `name` and `description` fields (description drives LLM trigger matching)
2. **Context section** — background info the agent needs (e.g., KServe's services, target industries)
3. **Workflow steps** — numbered steps with Worker → Checker → Orchestrator pattern
4. **Platform-adaptive execution** — PARALLEL mode (Claude Code, OpenCode, Codex) vs SEQUENTIAL mode (Claude.ai)
5. **Output format template** — exact structure the skill should produce

### Multi-Agent Pattern (used in company-research)

- **Worker**: Performs the research/action for a single step
- **Checker**: Validates worker output against 7 criteria (source present, credible, recent, accurate, complete, source diverse, BD-relevant); max 2 retries
- **Orchestrator**: Assembles final output after all workers complete; verifies Wave 2 steps ran after Wave 1

### Adding a New Skill

1. Create `<skill-name>/SKILL.md`
2. Add YAML frontmatter with `name` and `description`
3. Write the implementation instructions in Markdown
4. The npm `files` field (`"*/"` in package.json) auto-includes new skill directories

## Key Files

- `company-research/SKILL.md` — the primary skill (~950+ lines); reference for skill authoring patterns. Step 8 has 5 sub-sections (8A–8E). New steps added: 6B (Decision-Maker Dossiers), 7B (Job Postings), 7C (Technology Stack), 10B (ICP Score). PARALLEL mode uses explicit two-wave spawning.
- `package.json` — npm package metadata; `files: ["*/", "!node_modules/"]` auto-includes all skill dirs
- `README.md` — installation instructions and skill listing
