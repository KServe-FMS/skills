# Company Research Skill — Enterprise ROADMAP Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Replace `ROADMAP.md` with a comprehensive 7-phase enterprise master document (~120+ items) that is the single source of truth for elevating the company-research skill to enterprise grade.

**Architecture:** This is a documentation task, not a code task. Each task produces a self-contained chunk of the new `ROADMAP.md`. Task 1 runs the skill-creator audit; Tasks 2–6 write the ROADMAP in phase-grouped commits; Task 7 finalizes. All content is pre-enumerated below — no invention required. The executor assembles the file from the plan's content blocks.

**Tech Stack:** Markdown, git. No build step — changes take effect immediately in this skills repo.

---

## Task 1: Run Skill-Creator Audit

**Files:**
- Read: `company-research/SKILL.md`
- Produce: a list of Phase 7 items (carried into Task 6)

- [ ] **Step 1: Invoke the skill-creator skill**

Run:
```
Use the skill-creator:skill-creator skill to audit company-research/SKILL.md
against skill standards. Ask it to check:
- YAML frontmatter and trigger description quality
- Step naming consistency and numbering integrity
- Checker criteria coverage parity across all steps
- PARALLEL/SEQUENTIAL behavioral equivalence
- Source Priority table completeness and fallback coverage
- Output format template completeness (every step has a corresponding output section)
- Cross-reference accuracy (step numbers, wave assignments, orchestrator dependencies)
- Any structural anti-patterns or gaps
```

- [ ] **Step 2: Record audit findings**

After skill-creator completes, copy its findings into a scratch list. Each finding becomes a `- [ ]` item in Phase 7 with this format:
```
- [ ] **[Finding title]** — [what to fix/add] — [why it matters for skill correctness or BD quality]
      *(audit finding: "[verbatim or paraphrased finding from skill-creator]")*
```

- [ ] **Step 3: Verify Phase 7 has at least 10 items**

If skill-creator produced fewer than 10 findings, supplement with the known gaps listed in Task 6 (Phase 7 pre-enumerated items). Merge audit findings with pre-enumerated items, removing duplicates.

---

## Task 2: Write ROADMAP.md — Header + Phase 1

**Files:**
- Create (overwrite): `ROADMAP.md`

- [ ] **Step 1: Write the file header**

Write the following as the top of the new `ROADMAP.md`:

```markdown
# Company Research Skill — Enterprise ROADMAP

This is the enterprise master document for the `company-research` skill. It is the single source of truth for all shipped features and forward-looking improvements.

**Current skill version:** v1.4.0
**How to read this doc:** `[x]` = shipped · `[ ]` = roadmap · items are grouped by theme and roughly ordered by impact within each group · shipped items include `*(shipped: ...)` notes for traceability

---
```

- [ ] **Step 2: Write Phase 1 header + New Data Modules sub-section**

Append:

```markdown
## Phase 1 — Research Coverage

### New Data Modules (new steps)
- [x] **Employee Headcount & Growth Trend** — LinkedIn `#employees` over time; signals scaling pain or hiring freeze *(shipped: Step 7B extension)*
- [x] **Technology Stack Detection** — BuiltWith/Wappalyzer + job postings to detect CRMs, ERPs, cloud providers; reveals digital maturity and integration opportunities *(shipped: Step 7C)*
- [x] **Current Outsourcing Vendors** — detect competitors already embedded via news/announcements; changes the pitch angle entirely *(shipped: Step 16)*
- [x] **Job Postings as Intent Signals** — live roles on Naukri/LinkedIn reveal what they're hiring vs. what KServe could replace or augment *(shipped: Step 7B)*
- [x] **Regulatory & Legal Risk** — MCA compliance defaults, consumer court cases, SEBI/RBI notices; distress is both risk and opportunity *(shipped: Step 14 extension)*
- [x] **Competitive Landscape** — top 3 competitors; positions KServe to cite relevant case studies *(shipped: Step 17)*
- [x] **Key Partnerships & Integrations** — strategic alliances signal direction and potential entry points *(shipped: Step 14 extension)*
- [ ] **Import/Export Data** — Zauba/Volza trade activity; relevant for logistics and supply chain verticals — high-volume importers/exporters have complex back-office needs KServe can absorb
- [ ] **News Sentiment Scoring** — score news articles from the last 12 months as Positive / Neutral / Negative and classify trend direction — a worsening news sentiment curve is a stronger outreach hook than a static mention count
- [ ] **Patent & IP Activity** — search the Indian Patent Office (ipindia.gov.in) for recent filings — signals R&D investment and product-first culture, which shifts the pitch angle from back-office toward market research and lead generation
- [ ] **ESG / Sustainability Signals** — check for CSR filings (MCA Schedule VII), sustainability reports, and BRSR disclosures for listed companies — ESG-committed companies face higher compliance documentation load, a direct KServe back-office opportunity
```

- [ ] **Step 3: Write Phase 1 — Depth Improvements sub-section**

Append:

```markdown
### Depth Improvements to Existing Steps
- [x] **Step 6 — Directors** — add LinkedIn profile URLs, tenure, career history, and public quotes; currently only static MCA data *(shipped: Enhancement 2.1 + Step 6B)*
- [x] **Step 8 — Reviews** — add sentiment trend over time (improving or worsening?), not just themes; a worsening trend is a stronger trigger signal *(shipped: Enhancement 2.3)*
- [x] **Step 13 — Tracxn** — add Crunchbase employee count, funding timeline, and investor tier classification; currently too shallow *(shipped: Enhancement 2.4)*
- [x] **Step 14 — M&A** — extend to government contracts/tenders (GEM portal) and PE ownership structure *(shipped: Enhancement 2.5)*
- [ ] **Step 12 — Social Media Depth** — add posting frequency trend, content themes, and paid ad activity via Facebook Ad Library — paid ad spend is a direct proxy for marketing budget availability and digital maturity
- [ ] **Step 8A — App Store Trend Analysis** — extend app review analysis to detect version-specific rating spikes (a sudden drop tied to a specific app version = known product regression) — version-correlated problems signal an ops team under pressure
- [ ] **Step 6 — Board Composition Signal** — classify board as Founder-dominated / Institutional / Mixed and note implications for decision-making speed — founder-dominated boards close faster; institutional boards require multi-stakeholder buy-in
- [ ] **Step 3 — Turnover Trend (3-Year)** — pull 3 consecutive years of MCA revenue filings instead of just the latest — a declining revenue trend changes the pitch from growth-support to cost-reduction
- [ ] **Step 7B — Attrition Signal from JDs** — flag JDs that mention "replacement hire," "immediate joiners," or "notice period buyout" as high-attrition signals — high attrition in a function KServe serves is a direct outsourcing trigger
```

- [ ] **Step 4: Write Phase 1 — India-Primary Additions sub-section**

Append:

```markdown
### India-Primary Additions
- [ ] **GST Registration & Compliance Status** — search the GSTIN database for registration status, return-filing compliance, and any cancellation or suspension notices — GST non-compliance signals working capital stress and is an outsourcing receptivity trigger
- [ ] **EPFO Filing Signals** — cross-reference EPFO monthly employer ECR filings to triangulate actual headcount independent of LinkedIn estimates — more reliable for blue-collar-heavy industries where LinkedIn employee counts are systematically understated
- [ ] **CIBIL / Credit Bureau Risk Flag** — search for public CIBIL defaulter mentions, RBI NPA classification, or SARFAESI action — high credit risk is a distress signal that makes cost-reduction pitches (KServe's collections and back-office) immediately relevant
- [ ] **eCourts & NCLAT Case Search** — search eCourts India for active civil/commercial cases and NCLAT for insolvency/winding-up proceedings — active litigation signals operational stress and may indicate a freeze on new vendor commitments
- [ ] **Startup India / DPIIT Recognition Status** — check DPIIT startup recognition certificate status — recognized startups get regulatory relaxations and disproportionately need scale-without-headcount solutions that KServe provides
- [ ] **GeM Supplier Profile Depth** — extend Step 14 GeM check with bid history, active tenders, and awarded contract values — government contract volume signals compliance maturity and procurement cycle length, both of which shape the KServe pitch approach
- [ ] **SEBI Listed Entity Depth** — for BSE/NSE-listed companies, pull shareholding pattern, promoter pledge percentage, and quarterly results trend — promoter pledge above 50% is a financial stress indicator that elevates outsourcing receptivity
- [ ] **CIN-Level Subsidiary & Group Mapping** — search MCA for all entities sharing the same promoter DIN to reveal group company structure — group presence expands the total addressable relationship: win one entity, pitch the group
- [ ] **Regional Language Review Mining** — search for reviews on Sharechat, Koo, regional Facebook groups (Hindi/Marathi/Tamil/Telugu), and local forums — captures sentiment invisible on English-only platforms, especially relevant for tier-2/3 city brands
- [ ] **Tier-2/3 City Intelligence** — for companies with significant non-metro operations, check local IndiaMart regional listings, JustDial city-level pages, and local news — tier-2 operations often have weaker customer service infrastructure, a stronger KServe entry point
- [ ] **NASSCOM / FICCI / CII / ASSOCHAM Membership** — check industry body membership and conference speaking history — shared membership creates warm referral angles; speaking history reveals the executive's thought leadership priorities
- [ ] **ROC Annual Return Depth** — extend MCA lookup to include MGT-7 annual return for related-party transactions and significant changes in shareholding — related-party transaction volume signals group complexity that increases back-office load
```

- [ ] **Step 5: Write Phase 1 — Global Company Support sub-section**

Append:

```markdown
### Global Company Support (secondary capability)
*These items extend the skill for non-India prospects. They do not change India-first behavior — they activate when the company's primary registration is outside India.*

- [ ] **Global Registry Adapter** — detect the company's home country and route to the appropriate registry: Companies House (UK), SEC EDGAR (US), ASIC (Australia), ACRA (Singapore), RCS (France), Handelsregister (Germany) instead of MCA — registry-agnostic research enables KServe to pursue international accounts without manual source substitution
- [ ] **Multi-Currency Revenue Normalization** — convert foreign-currency revenue to INR at filing-date exchange rate with source citation — enables ICP Score comparison across geographies without apples-to-oranges revenue band errors
- [ ] **International Review Platforms** — add G2, Capterra, Software Advice, BBB (US), Trustpilot Global, ProductReview (AU), and Yelp to Step 8's source table for non-India companies — review coverage should not degrade when researching a global prospect
- [ ] **Global Job Boards** — add LinkedIn Global, Glassdoor Jobs, Indeed.com (global), Seek (AU), Reed (UK), and StepStone (EU) to Step 7B source table — hiring signals are geography-agnostic; the same KServe-relevant role detection logic applies
- [ ] **International Regulatory Risk Signals** — check SEC enforcement orders (US), FCA Financial Services Register (UK), ASIC infringement notices (AU), GDPR fines (EU via GDPR.eu enforcement tracker), and OFAC sanctions list — analogous to MCA/SEBI/RBI checks; regulatory distress creates urgency regardless of geography
- [ ] **Global BPO Vendor Detection** — extend Step 16 vendor search to include international BPO names (Accenture BPO, WNS, Concentrix, Teleperformance, EXL, Sutherland, Conduent) in addition to India-focused vendors — displacement pitch angle and differentiation argument change materially for global incumbent vendors
- [ ] **International News Coverage** — add Reuters, Bloomberg, FT, WSJ, TechCrunch, and local country-specific business press to Step 14 source table for non-India companies — ET/Mint/Business Standard do not cover global companies at depth
- [ ] **Country-Specific ICP Score Calibration** — adjust ICP Score revenue band thresholds for non-India companies (sweet spot: $5M–$100M USD equivalent rather than ₹50–500 Cr) — prevents systematic ICP score errors when comparing USD/EUR revenue against INR-calibrated thresholds
```

- [ ] **Step 6: Commit Phase 1**

```bash
git add ROADMAP.md
git commit -m "feat(roadmap): Phase 1 — Research Coverage enterprise expansion

Adds 4 new data modules, 5 depth improvements, 12 India-primary
additions, and 8 global company support items. Preserves all 7
shipped items verbatim.

Co-Authored-By: Claude Sonnet 4.6 <noreply@anthropic.com>"
```

---

## Task 3: Write ROADMAP.md — Phases 2 & 3

**Files:**
- Modify: `ROADMAP.md` (append)

- [ ] **Step 1: Write Phase 2 — BD Intelligence**

Append:

```markdown
---

## Phase 2 — BD Intelligence

- [x] **ICP Scoring** — quantified Ideal Customer Profile score (1–100) combining company size, industry match, pain points, growth signals, and tech maturity; gives BD a ranked priority list *(shipped: Step 10B)*
- [x] **Account Tiering** — classify as Tier 1 / 2 / 3 with explicit criteria so BD knows whether to assign a senior AE or an SDR *(shipped: Step 10B tier thresholds)*
- [x] **Decision-Maker Dossiers** — for each BD-relevant director, a 3-line brief: background, LinkedIn activity pattern, likely objection *(shipped: Step 6B)*
- [x] **Next Best Action** — a single ranked recommendation synthesizing all research into one concrete action (e.g., "Call the COO first — 3 open CX JDs on Naukri") *(shipped: Step 15E)*
- [ ] **Deal Size Estimation** — estimate outsourcing contract value range based on headcount, revenue band, and service fit — helps BD prioritize pipeline and set realistic quota expectations before the first call
- [ ] **BANT Pre-Qualification** — structured Budget / Authority / Need / Timeline scoring using research findings (revenue/funding for B, director mapping for A, pain points for N, growth events for T) — formats research output for direct CRM entry and pipeline qualification workflows
- [ ] **Personalized Outreach Templates** — one email draft per top decision-maker using research findings as hooks (not generic copy) — removes the SDR copywriting step and increases open rates through specificity
- [ ] **Competitive Positioning Brief** — if Step 16 detects an incumbent BPO vendor, generate a structured displacement argument: incumbent weakness → KServe advantage → proof point — converts vendor intelligence into a ready-to-use pitch narrative
- [ ] **Expanded Objection Bank** — extend Step 15D from 2–3 objections to a full bank of 8–10 covering: cost, trust, data security, incumbent loyalty, cultural fit, past bad BPO experience, internal capacity belief, and timing — gives reps a full prep sheet, not just the top two
- [ ] **Multi-Stakeholder Influence Map** — for companies with 3+ ★-flagged directors, map the reporting chain and decision-making influence relationships — knowing whether the CFO reports to the MD or operates independently changes which executive to open with
- [ ] **Outreach Sequence Builder** — generate a 3-touch outreach sequence (email → LinkedIn → call) with specific research hooks for each touch — removes guesswork for SDRs running high-volume campaigns without losing personalization
- [ ] **Win/Loss Signal Classification** — classify the prospect as Hot / Warm / Cold based on convergence of trigger signals (ICP score + active job postings + recent growth event) — distills the full research picture into a single traffic-light for BD triage
- [ ] **LinkedIn Message Templates** — generate ready-to-use LinkedIn InMail drafts (≤300 characters) for each ★-flagged director, anchored to a specific research finding — high-personalization at scale without requiring the SDR to read the full report
- [ ] **Cold Email Subject Line Generator** — output 3 subject line variants per prospect ranked by specificity (most specific: direct research finding; mid: industry + pain; generic: fallback) — subject line is the highest-leverage variable in cold email conversion
- [ ] **Industry-Specific Pitch Angle** — map the company's primary industry (from Step 2) to KServe's strongest vertical proof points — a BFSI pitch (collections, compliance documentation) is structurally different from an eCommerce pitch (returns processing, customer care volume)
- [ ] **Referral Angle Detector** — if Step 14 Key Partnerships includes any company KServe already serves, flag it and draft a referral-ask line — warm introductions via shared partners are the highest-conversion channel and currently go undetected
- [ ] **Re-Engagement Trigger Brief** — for Tier 3 / Deprioritize prospects, define exactly what event should trigger re-engagement (next funding round, leadership change, review spike, new KServe-relevant job postings) — turns a dead lead into a monitored lead with explicit conditions
- [ ] **Executive Relationship Score** — rate decision-maker accessibility as Easy / Moderate / Hard based on LinkedIn profile visibility, tenure at company, and recent post activity — helps SDRs prioritize outreach channel (InMail vs. phone vs. referral)
- [ ] **Account Health Score (post-onboarding)** — design a refresh-mode metric that re-runs key signals (reviews, headcount, job postings) after KServe wins the account to detect churn risk — proactive retention intelligence, not just acquisition intelligence
- [ ] **Competitive Urgency Signal** — if Step 17 shows a direct competitor is larger or better-funded and growing faster, flag it as a competitive urgency hook — "your competitor is scaling on outsourced ops; you're not" is a specific, time-sensitive trigger
```

- [ ] **Step 2: Write Phase 3 — Data Quality & Validation**

Append:

```markdown
---

## Phase 3 — Data Quality & Validation ✅ COMPLETE (shipped in v1.0.2 — 2026-03-09)

- [x] **Per-Field Confidence Scoring** — replace single overall confidence level with per-field scores (e.g., `Turnover: HIGH [MCA-verified]`, `Headcount: LOW [LinkedIn estimate]`) *(shipped)*
- [x] **Per-Field Freshness Timestamps** — each data point carries its source date, not just a report-level "data age" summary *(shipped)*
- [x] **Source Diversity Enforcement** — Checker flags over-reliance on a single aggregator; require at least 2 independent sources for high-confidence fields *(shipped)*
- [x] **Contradiction Detection Protocol** — explicit logic for revenue contradictions across sources, director mismatches, date inconsistencies *(shipped)*
- [x] **BD Relevance Checker Criterion** — "Does this output answer: *why should KServe reach out NOW?*"; prevents technically complete but strategically empty sections from passing *(shipped)*
- [x] **Anti-Hallucination Guardrail** — explicit instruction: if search returns zero results, Worker must state "No results found" — not infer from context *(shipped)*
- [x] **Retry Budget Surface** — when a Worker exhausts its 2-retry limit, the Orchestrator must receive and flag that exhaustion explicitly in the final report *(shipped)*
- [ ] **Confidence Decay Over Time** — flag data points older than 6 months as `Confidence: STALE` with a recommendation to re-verify — prevents stale ICP scores from driving outreach decisions months after the report was generated
- [ ] **Cross-Step Contradiction Matrix** — automatically detect contradictions between steps (e.g., Step 3 revenue vs. Step 7B headcount implying an implausible revenue-per-employee ratio) — surfaces data integrity issues before the BD rep uses the report
- [ ] **Field-Level Staleness Alerts** — attach a "data age" warning to individual fields (not just the footer) when the source date is >6 months old — makes staleness visible at the point of use, not buried in the footer
- [ ] **Third-Party Data Freshness SLA** — define a maximum acceptable source age per field type (Director data: 30 days / Revenue: 12 months / Social followers: 7 days) — enables Checker to enforce recency consistently across all Workers
- [ ] **Hallucination Detection: Revenue-per-Employee Plausibility Check** — flag Workers that report a revenue figure implying an implausible revenue-per-employee ratio (e.g., ₹10,000 Cr with 50 employees) — catches LLM interpolation errors before they reach the BD rep
- [ ] **Source Archiving Instruction** — instruct Workers to note if a source URL returns a 404 or has materially changed since the report was run — enables source recovery and audit trail for compliance reviews
- [ ] **Conflicting Source Resolution Log** — when sources conflict, require Worker to log all versions in a structured table (Source A vs. Source B vs. Authority winner with rationale) — makes resolution reasoning auditable and reproducible
- [ ] **DATA QUALITY Scorecard Expansion** — extend the DATA QUALITY footer with: total sources cited, total unique domains, share of MCA-verified fields, and newest source date alongside oldest — gives a richer reliability picture at a glance
```

- [ ] **Step 3: Commit Phases 2 & 3**

```bash
git add ROADMAP.md
git commit -m "feat(roadmap): Phases 2 & 3 — BD Intelligence + Data Quality expansion

Phase 2: 4 shipped items + 16 new BD intelligence items.
Phase 3: 7 shipped items + 8 new data quality items.

Co-Authored-By: Claude Sonnet 4.6 <noreply@anthropic.com>"
```

---

## Task 4: Write ROADMAP.md — Phases 4 & 5

**Files:**
- Modify: `ROADMAP.md` (append)

- [ ] **Step 1: Write Phase 4 — Workflow & Architecture**

Append:

```markdown
---

## Phase 4 — Workflow & Architecture

- [x] **Streaming Partial Delivery** — in SEQUENTIAL mode, present each completed section immediately rather than buffering until all steps finish *(shipped: Enhancement 2.8)*
- [x] **Formal Dependency Graph** — declare a DAG for PARALLEL mode; explicit two-wave spawning enforces Step 10/10B dependency *(shipped: Fix 1.2 + Orchestrator validation step)*
- [x] **Live Progress Reporting** — in PARALLEL mode, a status board after Wave 1 spawn; per-step ✓ updates as Workers complete *(shipped: Enhancement 2.7)*
- [x] **Rate Limit Awareness** — detect 429/throttle responses from Tracxn and LinkedIn; switch sources immediately rather than retrying the same endpoint *(shipped: Enhancement 2.6)*
- [x] **Graceful Partial Report** — if 4+ steps fail, Step 15 opens with a partial-data warning header *(shipped: Fix 1.4)*
- [ ] **Batch Mode** — research a list of companies (CSV/list input) in a single invocation, one report per company — critical for vertical campaign execution; BD teams need to process prospect lists, not single companies
- [ ] **Refresh/Delta Mode** — re-research a previously profiled company, surfacing only what changed since the last report — reduces research time for account managers re-engaging a prospect and highlights new trigger events
- [ ] **Watchlist/Monitor Mode** — periodically re-check a shortlisted prospect for trigger events (funding round, leadership change, bad press spike, new KServe-relevant job postings) — converts a nurture list into an active signal feed
- [ ] **Tool Availability Detection** — if a primary search tool is unavailable (not rate-limited, but absent entirely), explicitly try the secondary, then note the gap — prevents silent failures that produce incomplete reports without flagging the cause
- [ ] **Step Timeout Handling** — define a maximum execution time per Worker (recommended: 90 seconds); if exceeded, Worker submits best-available output with a `⚠️ TIMEOUT` note rather than blocking the pipeline indefinitely
- [ ] **Partial-Run Resume Protocol** — if a PARALLEL run is interrupted mid-wave, define a resume protocol: completed Workers' outputs are cached and re-used; only incomplete Workers re-run — prevents full re-research on interruption
- [ ] **SEQUENTIAL → PARALLEL Auto-Upgrade Detection** — at runtime, detect if the executing platform has gained subagent capability since SEQUENTIAL was assumed; offer to re-run in PARALLEL for speed — prevents users from running slow sequential mode on platforms that support parallelism
- [ ] **Source Failover Chain Automation** — if a Worker's primary source returns 429/access-denied, automatically advance to the next source in the Step's Source Priority table without returning to user — currently documented as a principle but not mechanically enforced
- [ ] **Worker Output Schema Validation** — after each Worker completes, validate output against a per-step schema (required fields present, source cited, confidence label present) — prevents malformed Worker output from reaching the Checker and causing downstream errors
- [ ] **Dependency-Aware Wave Scheduling** — extend the Wave 1 / Wave 2 model to support finer-grained internal dependencies (Step 9 must wait for Step 8; Step 6B must wait for Step 6; Step 10B must wait for Step 10) — currently these are implicit; making them explicit prevents race conditions in PARALLEL mode
- [ ] **Idempotent Re-Run Support** — define behavior when the same company is researched twice in the same session; deduplicate outputs and flag if cached data is <24 hours old — prevents duplicate API consumption and conflicting report versions
- [ ] **Orchestrator Completeness Health Check** — before assembling the final report, Orchestrator runs a structured completeness checklist: all 16 research steps present, Wave 2 ran post-Sanitizer, no steps in pending state, all RETRY_EXHAUSTED signals collected — currently partially specified; formalizing prevents silent omissions in edge cases
- [ ] **Worker Concurrency Limit** — define a maximum number of simultaneous Workers for platforms with rate limits (recommended: 8 concurrent) — prevents burst-spawning that triggers platform-level throttling and cascading failures
```

- [ ] **Step 2: Write Phase 5 — Output & Delivery**

Append:

```markdown
---

## Phase 5 — Output & Delivery

- [ ] **CRM-Ready JSON Export** — structured JSON block alongside the markdown report with field-mapped data ready for Salesforce/HubSpot/Zoho import — enables zero-friction CRM entry without manual copy-paste of research findings
- [ ] **Executive 1-Pager** — condensed output variant (≤300 words) for leadership review: ICP score, top 2 service fits, Next Best Action, and one risk flag — senior leadership doesn't read full reports; this format drives decisions at the top
- [ ] **Campaign Pitch Brief** — templated output optimized for cold outreach sequencing: Subject line → Hook (specific research finding) → Proof point (KServe case study angle) → CTA — removes the SDR copywriting step entirely
- [ ] **Risk Flag Consolidation Section** — explicit consolidated risk flags at the top of the report: acquisition freeze signal, regulatory risk, review spike, PE exit pressure — currently buried across individual step outputs; surfacing them up-front prevents BD reps from missing critical signals
- [ ] **Audit Trail** — log each source URL, timestamp, and which step consumed it in a structured appendix — enables compliance review and source traceability for enterprise clients who ask how the intelligence was gathered
- [ ] **Markdown → PDF/HTML Rendering Instruction** — add an explicit note to the report instructing the user how to render it as a formatted PDF or HTML page using the platform's export capability — makes reports shareable with non-AI-platform stakeholders
- [ ] **Multi-Language BD Briefing** — generate the BD Intelligence Briefing section (Step 15) in the prospect's primary business language alongside English — relevant for regional language prospects in India (Hindi, Marathi, Tamil) and for global accounts where English is not the business language
- [ ] **Report Version History** — track the date when a company was last researched and attach a diff summary when a report is re-run — enables account managers to quickly identify what triggered re-engagement
- [ ] **Report Summary Tile** — a 5-field at-a-glance card (Company, ICP Score, Top Service Fit, Next Best Action, Data Freshness) for use in Slack digests or CRM dashboard views — gives BD managers a portfolio-level view without opening individual reports
- [ ] **Confidence-Weighted Report Narrative** — adjust narrative confidence language based on field confidence levels (HIGH → stated as fact; MED → "signals suggest"; LOW → "early indication") — prevents BD reps from presenting LOW-confidence data as certain facts during client conversations
- [ ] **Customizable Section Toggle** — allow the user to request a subset of sections (e.g., "just the BD Briefing and ICP Score") without running all 16 steps — reduces research time for targeted use cases like quick pre-call prep
- [ ] **Timestamped Source Cache** — attach a retrieval timestamp to each cited source URL in the report — enables a future "source freshness check" run that detects broken or updated sources without re-running full research
```

- [ ] **Step 3: Commit Phases 4 & 5**

```bash
git add ROADMAP.md
git commit -m "feat(roadmap): Phases 4 & 5 — Workflow/Architecture + Output/Delivery expansion

Phase 4: 5 shipped items + 13 new workflow items.
Phase 5: 0 shipped + 12 new output/delivery items.

Co-Authored-By: Claude Sonnet 4.6 <noreply@anthropic.com>"
```

---

## Task 5: Write ROADMAP.md — Phase 6

**Files:**
- Modify: `ROADMAP.md` (append)

- [ ] **Step 1: Write Phase 6 — Platform & Integration**

Append:

```markdown
---

## Phase 6 — Platform & Integration

- [ ] **CRM Record Creation** — post-research, offer to create a CRM record via API (Salesforce/HubSpot/Zoho) using the JSON export from Phase 5 — zero-friction pipeline entry; the research run and CRM record creation become a single action
- [ ] **Slack/Email Delivery** — send the completed report (or the Summary Tile from Phase 5) to a team Slack channel or the BD rep's inbox — useful for async/batch research runs where the rep isn't watching the terminal
- [ ] **Multi-Language Output** — generate the BD briefing section in the prospect's primary business language alongside English — extends the multi-language item from Phase 5 with a platform-delivered bilingual format
- [ ] **Webhook Trigger Output** — after completing a research run, POST a structured payload to a configured webhook URL — enables integration with n8n, Zapier, Make.com, or custom pipelines without requiring CRM API credentials
- [ ] **API-First Output Schema** — define and document a stable JSON schema for the research report output (field names, types, nested objects) — enables programmatic consumption by downstream tools without brittle markdown parsing
- [ ] **HubSpot Native Integration** — map research output fields to HubSpot Contact and Company object properties and auto-populate via HubSpot API — highest-priority CRM integration given KServe's likely stack; reduces data entry to zero
- [ ] **Salesforce Integration** — map to Salesforce Lead and Account object fields; expose as a Flow-callable action — covers enterprise BD teams running on SFDC who cannot switch CRMs
- [ ] **Google Sheets Export** — write research output to a new Google Sheet row with column headers matching the report sections — accessible to teams not using a formal CRM; enables lightweight prospect tracking without additional tooling
- [ ] **Notification Trigger for Watchlist Events** — when Watchlist/Monitor Mode (Phase 4) detects a trigger event, push a notification to Slack or email with the specific signal and the recommended action from Step 15E — turns passive monitoring into active BD prompts
- [ ] **MCP Server Interface** — expose the company-research skill as an MCP tool callable from Claude Desktop, Cursor, or any MCP-compatible client — extends reach beyond Claude Code and Claude.ai to the full MCP ecosystem without skill duplication
```

- [ ] **Step 2: Commit Phase 6**

```bash
git add ROADMAP.md
git commit -m "feat(roadmap): Phase 6 — Platform & Integration expansion

10 new platform integration items covering CRM, Slack/email,
webhooks, API schema, and MCP interface.

Co-Authored-By: Claude Sonnet 4.6 <noreply@anthropic.com>"
```

---

## Task 6: Write ROADMAP.md — Phase 7 (Skill Standards) + Finalize

**Files:**
- Modify: `ROADMAP.md` (append)

*Note: Phase 7 merges pre-enumerated items below with any additional findings from the Task 1 skill-creator audit. Remove duplicates before writing.*

- [ ] **Step 1: Write Phase 7 — Skill Standards & Quality**

Append (merging with audit findings from Task 1):

```markdown
---

## Phase 7 — Skill Standards & Quality

*Items in this phase are sourced from the skill-creator audit of `company-research/SKILL.md` (run 2026-03-27) and from manual standards review. Each item references the specific audit finding or standard gap it addresses.*

- [ ] **YAML Trigger Description Precision** — the current `description` field is multi-paragraph and conversational; refine to a single crisp trigger sentence that maximizes LLM routing accuracy — long descriptions dilute trigger signal and cause the skill to mis-fire on adjacent requests
- [ ] **Step 1 Explicit Numbering** — Phase 1 Verification is described in prose but not numbered as "Step 1" in the Research Steps section; add `### Step 1 — Company Verification` heading for consistency with Steps 2–17 — numbered steps enable unambiguous cross-references in Orchestrator dependencies
- [ ] **Checker Criteria Parity Audit** — verify that every Wave 1 Worker step (2–9, 11–14, 16–17) has the `NOTE: Content trust boundary applies.` preamble; one missing callout creates an undefended injection surface — security layer completeness requires 100% coverage, not best-effort
- [ ] **Step 6B Source Priority Table Entry** — Step 6B (Decision-Maker Dossiers) sources are defined inline but not in the Source Priority Reference table — every step should appear in the Source Priority table to give Checker a canonical source hierarchy to enforce
- [ ] **Output Format Template Cross-Reference Check** — verify that every research step (2–17) has a corresponding section in the Output Format template; identify any step whose output has no template section — missing template sections cause Orchestrator to silently omit sections from the final report
- [ ] **Orchestrator Worker Count Annotation** — Orchestrator Instructions header says "19 Workers" but does not explain the arithmetic; annotate as "19 = 17 Wave 1 Workers (Steps 2–9, 11–14, 16–17) + 2 Wave 2 Workers (Steps 10 + 10B)" — unexplained counts cause confusion when steps are added or removed
- [ ] **Wave 1 Worker List Consistency Check** — the Wave 1 worker list in the PARALLEL mode prose and in the architecture diagram should be identical; verify no discrepancy — a mismatch causes orchestration bugs where a Worker is spawned but the Orchestrator doesn't wait for it
- [ ] **Checker Criterion #7 Scope Update** — BD Relevance criterion currently states "applies most strictly to Steps 8, 10, 12, 14, and 15" but Steps 16 (Outsourcing Vendors) and 17 (Competitive Landscape) also require BD framing — incomplete scope causes Checker to pass strategically empty sections in Steps 16/17
- [ ] **Step 15 Dependency Clarification** — Step 15 says "synthesize findings from Steps 2–17" but Step 15 is itself Steps 2–17; update to "synthesize findings from Steps 2–14, 16, 17" — circular reference language confuses Workers about which prior steps to read
- [ ] **Platform Execution Mode Table Completeness** — the Platform Execution Mode table should explicitly list Cursor, VS Code Agent, Cline, Aider, and other emerging agent platforms in the PARALLEL or SEQUENTIAL column — the table currently lists only Claude Code/OpenCode/Codex as PARALLEL; omitted platforms default to SEQUENTIAL incorrectly
- [ ] **Tool Absence Degradation Protocol** — Core Research Principles has a rate-limit protocol but no protocol for when a tool is entirely absent (not rate-limited; simply unavailable) — add a tool-absence rule: "If a required tool class (web search / file write / subagent) is unavailable, halt and notify the user before proceeding"
- [ ] **Injection Guard Criterion Retry Count Clarification** — Checker criterion #8 states injection redaction counts as one of the 2 allowed retries; verify this is unambiguous and does not conflict with the RETRY_EXHAUSTED signal definition — ambiguity here causes Workers to either under-retry (abandon too early) or over-retry (ignore the cap)
- [ ] **Step 10B Dependency Declaration Consistency** — Step 10B says it depends on "Steps 2–10" but its ICP Score dimensions reference only specific steps (2, 3, 6, 7, 7B, 8, 9, 10, 12, 14); update the dependency declaration to be explicit about which steps feed which dimensions — vague dependencies cause Wave 2 Workers to wait unnecessarily or spawn prematurely
- [ ] **Sanitizer Scope Documentation** — Sanitizer Instructions say "scan all approved Wave 1 outputs" but do not explicitly list which steps that covers (2–9, 11–14, 16–17); add the explicit step list — ambiguous scope causes Sanitizer to potentially skip steps
- [ ] **Skill Compatibility Statement Update** — the "Compatible with" line lists Claude.ai · Claude Code · Cowork · OpenCode · Codex; update to include Claude Desktop (MCP) and Cursor — compatibility claims should reflect the current platform landscape
```

- [ ] **Step 2: Write the final item count footer**

Append:

```markdown
---

**Total items: [COUNT]**
*(Count all items including shipped `[x]` and open `[ ]` across all 7 phases)*
```

Replace `[COUNT]` with the actual count after writing all phases.

- [ ] **Step 3: Verify item taxonomy compliance**

Scan the complete ROADMAP.md for any item that violates the taxonomy (title + description + rationale required). Fix any orphan titles (title only, no description). Check that every shipped item has its `*(shipped: ...)` note.

Run a quick count:
```bash
grep -c '^\- \[' ROADMAP.md
```

Verify the count matches the footer total.

- [ ] **Step 4: Final commit**

```bash
git add ROADMAP.md
git commit -m "feat(roadmap): Phase 7 — Skill Standards & Quality + finalize

Phase 7: 15 skill standards items from skill-creator audit.
Final ROADMAP.md: 7 phases, [COUNT] total items.
Replaces previous ROADMAP.md (46 items, 6 phases).

Co-Authored-By: Claude Sonnet 4.6 <noreply@anthropic.com>"
```

---

## Self-Review

**Spec coverage check:**

| Spec requirement | Plan task |
|---|---|
| Replace ROADMAP.md | Tasks 2–6 write + overwrite the file |
| Preserve all shipped `[x]` items | Task 2 Step 2, Task 3 Steps 1–2 copy all shipped items verbatim |
| 7 phases | Tasks 2–6 cover all 7 phases |
| ~135 items total | Enumerated: Phase 1 (~32) + Phase 2 (~20) + Phase 3 (~15) + Phase 4 (~18) + Phase 5 (~12) + Phase 6 (~10) + Phase 7 (~15) = ~122 pre-enumerated + audit findings = 125–135 |
| India-primary sub-sections in Phase 1 | Task 2 Steps 4–5 |
| Global Company Support sub-section | Task 2 Step 5 |
| Phase 7 from skill-creator audit | Task 1 runs audit; Task 6 Step 1 merges findings |
| Every item has title + description + rationale | All items in this plan follow the taxonomy; Task 6 Step 3 verifies |
| Commit the new ROADMAP.md | Every task ends with a commit step |

**Placeholder scan:** No TBDs, no TODOs, no "implement later." Every item has full content.

**Type consistency:** N/A — documentation task, no code types.

**Gaps:** None identified. All spec requirements have corresponding tasks.
