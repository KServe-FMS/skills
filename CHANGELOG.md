# Changelog

All notable changes to `@kserve/skills` are documented here.
Format follows [Keep a Changelog](https://keepachangelog.com/en/1.0.0/).

---

## [1.2.1] — 2026-03-12

### Fixed
- PARALLEL Wave 1 worker list now includes Steps 6B, 7B, 7C (was missing from text; diagram was already correct)
- Progress board template updated to "15 parallel workers" (was "12")
- Wave 2 announcement and Orchestrator dependency check now reference Steps 10 & 10B
- README: removed `npx skills add @kserve/skills` — skills CLI only supports GitHub `owner/repo` format; use `npx skills add KServe-FMS/skills`

---

## [1.2.0] — 2026-03-12

### Added — New Steps
- **Step 6B — Decision-Maker Dossiers**: 3-line brief per ★-flagged BD-relevant director: professional background, LinkedIn activity pattern, and likely first objection based on career history
- **Step 7B — Job Postings as Intent Signals**: searches Naukri, LinkedIn Jobs, and Indeed India for active roles; surfaces KServe-relevant openings (CS, Collections, Back-Office, Lead Gen) as outsourcing intent signals
- **Step 7C — Technology Stack Detection**: uses BuiltWith, Wappalyzer, and job posting mentions to identify CRM, customer support tool, review management tool, and marketing automation; surfaces integration BD angle
- **Step 10B — ICP Score**: 0–100 Ideal Customer Profile score across 10 dimensions (industry match, revenue band, employee proxy, pain point evidence, review quality, growth/change, decision-maker accessibility, job postings, social presence, data confidence); Tier 1/2/3/Deprioritize classification with recommended action
- **Step 15E — Next Best Action**: one specific, named, evidenced action for the BD rep (includes named director, channel, and research finding hook); Tier 3/Deprioritize falls back to nurture sequence with specific re-trigger conditions

### Added — Enhancements to Existing Steps
- **Step 6 — Directors**: LinkedIn profile URL, tenure, and ★ NEW flag (joined < 6 months) for each BD-relevant director; star (★) visual marker distinguishes decision-makers from board/independent directors
- **Step 8A & 8B — Reviews**: sentiment trend classification per sub-section (Improving / Worsening / Stable / Insufficient data) with 1-sentence observation
- **Step 9 — Rating**: sample size caveat — ratings based on < 15 reviews are marked Confidence: LOW; zero-review case documented explicitly
- **Step 10 — KServe Fit**: explicit HIGH/MEDIUM FIT decision rules with required evidence type for each; Exclude criteria with one-line Orchestrator note for omitted services
- **Step 12 — Social Media**: platform-calibrated engagement thresholds (LinkedIn < 0.5%, Instagram < 1.5%, Facebook/Twitter < 0.5%/0.3%); sample size documented; low-follower-base flag (< 1,000 all platforms)
- **Step 13 — Tracxn**: Crunchbase employee count range, per-round funding timeline, total funding raised, investor tier classification (Tier 1/2/Bootstrapped); BD signal per tier
- **Step 14 — M&A**: GeM portal supplier check; PE fund vintage and exit-horizon BD signal

### Added — Workflow Improvements
- **Two-wave PARALLEL spawning**: explicit Wave 1 (Workers 2,3,4,5,6,6B,7,7B,7C,8,9,11,12,13,14) and Wave 2 (Workers 10, 10B after all Wave 1 Checker-approved) — fixes race condition where Step 10 could run before Step 8 completed
- **PARALLEL progress status board**: status posted after Wave 1 spawn; per-step ✓ update as each Worker is approved; Wave 2 announcement before Orchestrator
- **SEQUENTIAL streaming delivery**: each step output appended immediately after Checker approval; no buffering until Step 15
- **Step 15 quality gate**: partial-data warning if ≥ 4 steps exhausted retries; Trigger Signals omitted if Step 10 RETRY_EXHAUSTED; review-based starters omitted if Step 8 RETRY_EXHAUSTED
- **Rate limit handling protocol**: max 1 retry per source → switch to next in priority table → flag ⚠️ in report; gated-source guidance for Tracxn, LinkedIn, MCA AOC-4

### Fixed
- Step 6 typo: "identify for BD outreach: directors likely to be decision-makers for BD outreach" → deduplicated
- Checker header said "five criteria" after criteria expanded to seven in v1.0.2 (now corrected throughout + SEQUENTIAL diagram updated)
- Orchestrator dependency check: added step 2 to verify Step 10 ran after Wave 1 complete before assembling
- Step 8E response speed: "Not determinable" now requires checking timestamp pairs on 3+ platforms before accepting; guidance added on where to find them (Google Business, Glassdoor, App Store)
- Source Priority table: Steps 9 and 15 now document synthesis fallback rules (partial-input handling)

### Changed
- Output Format template expanded from 16 to 20 sections; new sections: Decision-Maker Dossiers, Job Postings, Technology Stack, ICP Score, Next Best Action
- Tracxn section renamed to "Tracxn / Funding Profile"; M&A section renamed to "M&A, Funding & Ownership"
- PARALLEL mode diagram updated to show two-wave architecture
- Source Priority Reference table expanded with rows for Steps 6B, 7B, 7C, 10B

### Repository
- Added `CONTRIBUTING.md` with skill authoring guide, step numbering conventions, and versioning policy
- `README.md`: section count updated to 20; table updated with all new sections; versioning policy added
- `CLAUDE.md`: Checker criteria count corrected to 7; SKILL.md line count updated; two-wave PARALLEL architecture noted
- `ROADMAP.md`: Phase 3 marked ✅ COMPLETE; 10 additional items marked [x] as shipped in this release

---

## [1.1.0] — 2026-03-11

*(See git log for Step 8 five-section restructure details)*

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
