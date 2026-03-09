# Changelog

All notable changes to `@kserve/skills` are documented here.
Format follows [Keep a Changelog](https://keepachangelog.com/en/1.0.0/).

---

## [1.0.2] — 2026-03-09

### Added
- **Per-field confidence scoring** — every output section now carries `Confidence: HIGH/MED/LOW` inline
- **Per-field source freshness timestamps** — every section now shows `Source date: YYYY-MM-DD` alongside sources
- **Source diversity enforcement** — Checker criterion 6: high-stakes fields (Turnover, Directors, Head Office) require 2+ independent sources for a HIGH rating; Tofler + Zauba Corp correctly identified as non-independent (both pull from MCA)
- **BD relevance gate** — Checker criterion 7: sections must answer "why should KServe reach out NOW?" — not just factually correct, but strategically actionable
- **Contradiction detection protocol** — Checker proactively flags 4 common mismatch patterns: turnover FY/entity mismatch, director MCA-vs-website lag, founded-vs-incorporated date split, branch count triangulation
- **Anti-hallucination guardrail** — Core Research Principle: zero search results must be stated as "Not publicly available", never inferred from context or adjacent companies
- **RETRY_EXHAUSTED signal** — Checker surfaces structured `RETRY_EXHAUSTED: [Step N] — [field] — [reason]` signal to Orchestrator after 2 failed retries
- **Orchestrator data gap tally** — Orchestrator collects all RETRY_EXHAUSTED signals, tallies confidence levels across all 14 sections, and renders them in the DATA QUALITY footer
- **Updated DATA QUALITY footer** — now shows: overall confidence tally (e.g., `9/14 HIGH · 3 MED · 2 LOW`), data gaps list, oldest source date, and confidence key

### Changed
- Checker criteria expanded from 5 to 7
- DATA QUALITY footer changed from single overall rating to multi-field breakdown
- Conflict resolution hierarchy clarified: MCA > official website > major publications > aggregators

---

## [1.0.1] — 2026-02-28

### Changed
- Bumped npm package version to 1.0.1 for registry release

---

## [1.0.0] — 2026-02-26

### Added
- Initial release: `company-research` skill — BD intelligence research for KServe's sales team
- **14-step research workflow**: verification → line of business → turnover → head office → years in existence → directors → branches → reviews → rating → KServe fit → customer care → social media → Tracxn → M&A → BD briefing
- **Worker → Checker → Orchestrator** multi-agent architecture
- **PARALLEL mode** (Claude Code, OpenCode, Codex) and **SEQUENTIAL mode** (Claude.ai, Cowork) execution
- **Phase 1 company verification** — user confirms identity before research begins
- **MCA as ground truth** for Indian company data (incorporation date, directors, registered address, financials)
- **Source priority reference table** for all 14 steps
- **KServe services fit assessment** — 3–5 services ranked HIGH/MEDIUM fit with evidence from research
- **BD Intelligence Briefing** (Step 15) — things to know, conversation starters, trigger signals, objection responses
- **Platform-adaptive tool naming** — web_search/WebSearch/search/browse; write_file/Write/fs.write; Task/spawn_agent
- **Graceful degradation** — any step that hits a wall notes the gap and continues
- Structured output template with 14 labelled sections + DATA QUALITY footer
