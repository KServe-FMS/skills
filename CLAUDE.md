# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

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
- **Checker**: Validates worker output against 5 criteria (source present, credible, recent, accurate, complete); max 2 retries
- **Orchestrator**: Assembles final output after all workers complete

### Adding a New Skill

1. Create `<skill-name>/SKILL.md`
2. Add YAML frontmatter with `name` and `description`
3. Write the implementation instructions in Markdown
4. The npm `files` field (`"*/"` in package.json) auto-includes new skill directories

## Key Files

- `company-research/SKILL.md` — the primary skill (492 lines); reference for skill authoring patterns
- `package.json` — npm package metadata; `files: ["*/", "!node_modules/"]` auto-includes all skill dirs
- `README.md` — installation instructions and skill listing
