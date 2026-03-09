# KServe Skills

[![npm](https://img.shields.io/npm/v/@kserve/skills)](https://www.npmjs.com/package/@kserve/skills)

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

## How to use

Once installed, just ask naturally in any supported AI platform:

- `"Research Reliance Retail for BD"`
- `"Look up Bajaj Finance — potential outsourcing client"`
- `"Do a BD profile for Zepto, their website is zepto.co"`
- `"Get me info on this company: www.meesho.com"`
- `"Check out HDFC Ergo for a KServe pitch"`

The skill confirms the right company with you first, then runs the full research automatically.

## What you get

A structured BD intelligence report covering 14 sections:

| Section | What it contains |
|---|---|
| ✅ Verification | Confirmed company identity before research begins |
| 📋 Line of Business | Industry, business model (B2B/B2C/B2G), key segments |
| 💰 Turnover | Revenue in ₹ Crores with financial year and MCA source |
| 📍 Head Office | Registered address (MCA) cross-referenced with operating address |
| 📅 Years in Existence | Incorporation year and company age |
| 👔 Directors | MCA-verified names, DINs, and BD-relevant decision-makers |
| 🗺️ Branches & Offices | Location count, key cities, international presence |
| ⭐ Reviews & Reputation | Top 5 positives and negatives from the last 12 months |
| 🎯 Overall Rating | Synthesized reputation score (1–10) with rationale |
| 🤝 KServe Fit | 3–5 services ranked HIGH/MEDIUM fit with specific evidence |
| 📞 Customer Care | Published support number (or absence as a BD signal) |
| 📱 Social Media | Follower counts and engagement signal across platforms |
| 📊 Tracxn Profile | Startup score, funding stage, investors |
| 🔀 M&A & Funding | Recent acquisitions, funding rounds, PE activity |
| 🧠 BD Briefing | Conversation starters, trigger signals, objection responses |
| 📝 Data Quality | Per-field confidence (HIGH/MED/LOW), source dates, data gaps |

Every data point includes a source URL and freshness timestamp. High-stakes fields (turnover, directors) are MCA-verified.

## Adding New Skills

Drop a new directory with a `SKILL.md` file into this repo. The skills CLI will automatically discover it.

```
skills/
├── company-research/
│   └── SKILL.md
├── your-new-skill/      ← add here
│   └── SKILL.md
```

See [CHANGELOG.md](./CHANGELOG.md) for version history.
