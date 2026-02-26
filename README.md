# KServe Skills

Agent skills for KServe's business development and sales intelligence workflows.
Compatible with Claude Code, Claude.ai, OpenCode, Codex, and any platform that supports the [skills](https://github.com/vercel-labs/skills) standard.

## Install

```bash
npx skills add KServe-FMS/skills
```

Or from npm:

```bash
npx skills add @kserve/skills
```

Install a specific skill:

```bash
npx skills add KServe-FMS/skills --skill company-research
```

## Available Skills

| Skill | Description |
|---|---|
| `company-research` | Researches a prospect company and produces a full BD intelligence report — turnover, directors, reviews, KServe fit assessment, and actionable outreach briefing |

## Adding New Skills

Drop a new directory with a `SKILL.md` file into this repo. The skills CLI will automatically discover it.

```
skills/
├── company-research/
│   └── SKILL.md
├── your-new-skill/      ← add here
│   └── SKILL.md
```
