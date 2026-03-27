# Company Research Skill — Enterprise ROADMAP

This is the enterprise master document for the `company-research` skill. It is the single source of truth for all shipped features and forward-looking improvements.

**Current skill version:** v1.4.0
**How to read this doc:** `[x]` = shipped · `[ ]` = roadmap · items are grouped by theme and roughly ordered by impact within each group · shipped items include `*(shipped: ...)` notes for traceability

---

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

### Depth Improvements to Existing Steps
- [x] **Step 6 — Directors** — add LinkedIn profile URLs, tenure, career history, and public quotes; currently only static MCA data *(shipped: Enhancement 2.1 + Step 6B)*
- [x] **Step 8 — Reviews** — add sentiment trend over time (improving or worsening?), not just themes; a worsening trend is a stronger trigger signal *(shipped: Enhancement 2.3)*
- [x] **Step 13 — Tracxn** — add Crunchbase employee count, funding timeline, and investor tier classification; currently too shallow *(shipped: Enhancement 2.4)*
- [x] **Step 14 — M&A** — extend to government contracts/tenders (GEM portal) and PE ownership structure *(shipped: Enhancement 2.5)*
- [ ] **Step 6 — Board Composition Signal** — classify board as Founder-dominated / Institutional / Mixed and note implications for decision-making speed — founder-dominated boards close faster; institutional boards require multi-stakeholder buy-in
- [ ] **Step 3 — Turnover Trend (3-Year)** — pull 3 consecutive years of MCA revenue filings instead of just the latest — a declining revenue trend changes the pitch from growth-support to cost-reduction
- [ ] **Step 7B — Attrition Signal from JDs** — flag JDs that mention "replacement hire," "immediate joiners," or "notice period buyout" as high-attrition signals — high attrition in a function KServe serves is a direct outsourcing trigger
- [ ] **GeM Supplier Profile Depth** — extend Step 14 GeM check with bid history, active tenders, and awarded contract values — government contract volume signals compliance maturity and procurement cycle length, both of which shape the KServe pitch approach

### India-Primary Additions
- [ ] **GST Registration & Compliance Status** — search the GSTIN database for registration status, return-filing compliance, and any cancellation or suspension notices — GST non-compliance signals working capital stress and is an outsourcing receptivity trigger
- [ ] **EPFO Filing Signals** — cross-reference EPFO monthly employer ECR filings to triangulate actual headcount independent of LinkedIn estimates — more reliable for blue-collar-heavy industries where LinkedIn employee counts are systematically understated
- [ ] **CIBIL / Credit Bureau Risk Flag** — search for public CIBIL defaulter mentions, RBI NPA classification, or SARFAESI action — high credit risk is a distress signal that makes cost-reduction pitches (KServe's collections and back-office) immediately relevant
- [ ] **eCourts & NCLAT Case Search** — search eCourts India for active civil/commercial cases and NCLAT for insolvency/winding-up proceedings — active litigation signals operational stress and may indicate a freeze on new vendor commitments
- [ ] **Startup India / DPIIT Recognition Status** — check DPIIT startup recognition certificate status — recognized startups get regulatory relaxations and disproportionately need scale-without-headcount solutions that KServe provides
- [ ] **SEBI Listed Entity Depth** — for BSE/NSE-listed companies, pull shareholding pattern, promoter pledge percentage, and quarterly results trend — promoter pledge above 50% is a financial stress indicator that elevates outsourcing receptivity
- [ ] **CIN-Level Subsidiary & Group Mapping** — search MCA for all entities sharing the same promoter DIN to reveal group company structure — group presence expands the total addressable relationship: win one entity, pitch the group
- [ ] **Tier-2/3 City Intelligence** — for companies with significant non-metro operations, check local IndiaMart regional listings, JustDial city-level pages, and local news — tier-2 operations often have weaker customer service infrastructure, a stronger KServe entry point
- [ ] **NASSCOM / FICCI / CII / ASSOCHAM Membership** — check industry body membership and conference speaking history — shared membership creates warm referral angles; speaking history reveals the executive's thought leadership priorities
- [ ] **ROC Annual Return Depth** — extend MCA lookup to include MGT-7 annual return for related-party transactions and significant changes in shareholding — related-party transaction volume signals group complexity that increases back-office load

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

---

## Phase 2 — BD Intelligence

- [x] **ICP Scoring** — quantified Ideal Customer Profile score (1–100) combining company size, industry match, pain points, growth signals, and tech maturity; gives BD a ranked priority list *(shipped: Step 10B)*
- [x] **Account Tiering** — classify as Tier 1 / 2 / 3 with explicit criteria so BD knows whether to assign a senior AE or an SDR *(shipped: Step 10B tier thresholds)*
- [x] **Decision-Maker Dossiers** — for each BD-relevant director, a 3-line brief: background, LinkedIn activity pattern, likely objection *(shipped: Step 6B)*
- [x] **Next Best Action** — a single ranked recommendation synthesizing all research into one concrete action (e.g., "Call the COO first — 3 open CX JDs on Naukri") *(shipped: Step 15E)*
- [ ] **BANT Pre-Qualification** — structured Budget / Authority / Need / Timeline scoring using research findings (revenue/funding for B, director mapping for A, pain points for N, growth events for T) — formats research output for direct CRM entry and pipeline qualification workflows
- [ ] **Competitive Positioning Brief** — if Step 16 detects an incumbent BPO vendor, generate a structured displacement argument: incumbent weakness → KServe advantage → proof point — converts vendor intelligence into a ready-to-use pitch narrative
- [ ] **Expanded Objection Bank** — extend Step 15D from 2–3 objections to a full bank of 8–10 covering: cost, trust, data security, incumbent loyalty, cultural fit, past bad BPO experience, internal capacity belief, and timing — gives reps a full prep sheet, not just the top two
- [ ] **Multi-Stakeholder Influence Map** — for companies with 3+ ★-flagged directors, map the reporting chain and decision-making influence relationships — knowing whether the CFO reports to the MD or operates independently changes which executive to open with
- [ ] **Industry-Specific Pitch Angle** — map the company's primary industry (from Step 2) to KServe's strongest vertical proof points — a BFSI pitch (collections, compliance documentation) is structurally different from an eCommerce pitch (returns processing, customer care volume)
- [ ] **Re-Engagement Trigger Brief** — for Tier 3 / Deprioritize prospects, define exactly what event should trigger re-engagement (next funding round, leadership change, review spike, new KServe-relevant job postings) — turns a dead lead into a monitored lead with explicit conditions
- [ ] **Executive Relationship Score** — rate decision-maker accessibility as Easy / Moderate / Hard based on LinkedIn profile visibility, tenure at company, and recent post activity — helps SDRs prioritize outreach channel (InMail vs. phone vs. referral)
- [ ] **Competitive Urgency Signal** — if Step 17 shows a direct competitor is larger or better-funded and growing faster, flag it as a competitive urgency hook — "your competitor is scaling on outsourced ops; you're not" is a specific, time-sensitive trigger

---

## Phase 3 — Data Quality & Validation ✅ COMPLETE (shipped in v1.0.2 — 2026-03-09)

- [x] **Per-Field Confidence Scoring** — replace single overall confidence level with per-field scores (e.g., `Turnover: HIGH [MCA-verified]`, `Headcount: LOW [LinkedIn estimate]`) *(shipped)*
- [x] **Per-Field Freshness Timestamps** — each data point carries its source date, not just a report-level "data age" summary *(shipped)*
- [x] **Source Diversity Enforcement** — Checker flags over-reliance on a single aggregator; require at least 2 independent sources for high-confidence fields *(shipped)*
- [x] **Contradiction Detection Protocol** — explicit logic for revenue contradictions across sources, director mismatches, date inconsistencies *(shipped)*
- [x] **BD Relevance Checker Criterion** — "Does this output answer: *why should KServe reach out NOW?*"; prevents technically complete but strategically empty sections from passing *(shipped)*
- [x] **Anti-Hallucination Guardrail** — explicit instruction: if search returns zero results, Worker must state "No results found" — not infer from context *(shipped)*
- [x] **Retry Budget Surface** — when a Worker exhausts its 2-retry limit, the Orchestrator must receive and flag that exhaustion explicitly in the final report *(shipped)*
- [ ] **Cross-Step Contradiction Matrix** — automatically detect contradictions between steps (e.g., Step 3 revenue vs. Step 7B headcount implying an implausible revenue-per-employee ratio) — surfaces data integrity issues before the BD rep uses the report
- [ ] **Field-Level Staleness Alerts** — attach a "data age" warning to individual fields (not just the footer) when the source date is >6 months old — makes staleness visible at the point of use, not buried in the footer
- [ ] **Hallucination Detection: Revenue-per-Employee Plausibility Check** — flag Workers that report a revenue figure implying an implausible revenue-per-employee ratio (e.g., ₹10,000 Cr with 50 employees) — catches LLM interpolation errors before they reach the BD rep
- [ ] **Conflicting Source Resolution Log** — when sources conflict, require Worker to log all versions in a structured table (Source A vs. Source B vs. Authority winner with rationale) — makes resolution reasoning auditable and reproducible
- [ ] **DATA QUALITY Scorecard Expansion** — extend the DATA QUALITY footer with: total sources cited, total unique domains, share of MCA-verified fields, and newest source date alongside oldest — gives a richer reliability picture at a glance

---

## Phase 4 — Workflow & Architecture

- [x] **Streaming Partial Delivery** — in SEQUENTIAL mode, present each completed section immediately rather than buffering until all steps finish *(shipped: Enhancement 2.8)*
- [x] **Formal Dependency Graph** — declare a DAG for PARALLEL mode; explicit two-wave spawning enforces Step 10/10B dependency *(shipped: Fix 1.2 + Orchestrator validation step)*
- [x] **Live Progress Reporting** — in PARALLEL mode, a status board after Wave 1 spawn; per-step ✓ updates as Workers complete *(shipped: Enhancement 2.7)*
- [x] **Rate Limit Awareness** — detect 429/throttle responses from Tracxn and LinkedIn; switch sources immediately rather than retrying the same endpoint *(shipped: Enhancement 2.6)*
- [x] **Graceful Partial Report** — if 4+ steps fail, Step 15 opens with a partial-data warning header *(shipped: Fix 1.4)*
- [ ] **Tool Availability Detection** — if a primary search tool is unavailable (not rate-limited, but absent entirely), explicitly try the secondary, then note the gap — prevents silent failures that produce incomplete reports without flagging the cause
- [ ] **Partial-Run Resume Protocol** — if a PARALLEL run is interrupted mid-wave, define a resume protocol: completed Workers' outputs are cached and re-used; only incomplete Workers re-run — prevents full re-research on interruption
- [ ] **SEQUENTIAL → PARALLEL Auto-Upgrade Detection** — at runtime, detect if the executing platform has gained subagent capability since SEQUENTIAL was assumed; offer to re-run in PARALLEL for speed — prevents users from running slow sequential mode on platforms that support parallelism
- [ ] **Source Failover Chain Automation** — if a Worker's primary source returns 429/access-denied, automatically advance to the next source in the Step's Source Priority table without returning to user — currently documented as a principle but not mechanically enforced
- [ ] **Worker Output Schema Validation** — after each Worker completes, validate output against a per-step schema (required fields present, source cited, confidence label present) — prevents malformed Worker output from reaching the Checker and causing downstream errors
- [ ] **Dependency-Aware Wave Scheduling** — extend the Wave 1 / Wave 2 model to support finer-grained internal dependencies (Step 9 must wait for Step 8; Step 6B must wait for Step 6; Step 10B must wait for Step 10) — currently these are implicit; making them explicit prevents race conditions in PARALLEL mode
- [ ] **Idempotent Re-Run Support** — define behavior when the same company is researched twice in the same session; deduplicate outputs and flag if cached data is <24 hours old — prevents duplicate API consumption and conflicting report versions
- [ ] **Orchestrator Completeness Health Check** — before assembling the final report, Orchestrator runs a structured completeness checklist: all 16 research steps present, Wave 2 ran post-Sanitizer, no steps in pending state, all RETRY_EXHAUSTED signals collected — currently partially specified; formalizing prevents silent omissions in edge cases

---

## Phase 5 — Output & Delivery

- [ ] **CRM-Ready JSON Export** — structured JSON block alongside the markdown report with field-mapped data ready for Salesforce/HubSpot/Zoho import — enables zero-friction CRM entry without manual copy-paste of research findings
- [ ] **Risk Flag Consolidation Section** — explicit consolidated risk flags at the top of the report: acquisition freeze signal, regulatory risk, review spike, PE exit pressure — currently buried across individual step outputs; surfacing them up-front prevents BD reps from missing critical signals
- [ ] **Audit Trail** — log each source URL, timestamp, and which step consumed it in a structured appendix — enables compliance review and source traceability for enterprise clients who ask how the intelligence was gathered
- [ ] **Confidence-Weighted Report Narrative** — adjust narrative confidence language based on field confidence levels (HIGH → stated as fact; MED → "signals suggest"; LOW → "early indication") — prevents BD reps from presenting LOW-confidence data as certain facts during client conversations
- [ ] **Customizable Section Toggle** — allow the user to request a subset of sections (e.g., "just the BD Briefing and ICP Score") without running all 16 steps — reduces research time for targeted use cases like quick pre-call prep
- [ ] **Timestamped Source Cache** — attach a retrieval timestamp to each cited source URL in the report — enables a future "source freshness check" run that detects broken or updated sources without re-running full research

---

## Phase 6 — Platform & Integration

- [ ] **CRM Record Creation** — post-research, offer to create a CRM record via API (Salesforce/HubSpot/Zoho) using the JSON export from Phase 5 — zero-friction pipeline entry; the research run and CRM record creation become a single action
- [ ] **Slack/Email Delivery** — send the completed report (or the Summary Tile from Phase 5) to a team Slack channel or the BD rep's inbox — useful for async/batch research runs where the rep isn't watching the terminal
- [ ] **Webhook Trigger Output** — after completing a research run, POST a structured payload to a configured webhook URL — enables integration with n8n, Zapier, Make.com, or custom pipelines without requiring CRM API credentials
- [ ] **API-First Output Schema** — define and document a stable JSON schema for the research report output (field names, types, nested objects) — enables programmatic consumption by downstream tools without brittle markdown parsing
- [ ] **Google Sheets Export** — write research output to a new Google Sheet row with column headers matching the report sections — accessible to teams not using a formal CRM; enables lightweight prospect tracking without additional tooling
- [ ] **Notification Trigger for Watchlist Events** — when Watchlist/Monitor Mode (Phase 4) detects a trigger event, push a notification to Slack or email with the specific signal and the recommended action from Step 15E — turns passive monitoring into active BD prompts
- [ ] **MCP Server Interface** — expose the company-research skill as an MCP tool callable from Claude Desktop, Cursor, or any MCP-compatible client — extends reach beyond Claude Code and Claude.ai to the full MCP ecosystem without skill duplication

---

## Phase 7 — Skill Standards & Quality

*Items in this phase are sourced from the skill-creator audit of `company-research/SKILL.md` (run 2026-03-27) and from manual standards review.*

- [ ] **YAML Trigger Description Precision** — refine the 7-line conversational `description` field to a structured trigger statement that leads with the trigger signal rather than burying it — long descriptions dilute trigger signal and cause the skill to mis-fire on adjacent requests *(audit finding: "description is thorough but lists triggering phrases as examples at the end; should lead with the trigger signal")*
- [ ] **Step 1 Explicit Numbering** — add `### Step 1 — Company Verification` heading to the Research Steps section to match the numbered structure of Steps 2–17 — currently Step 1 exists only as prose in the Research Flow section, creating an off-by-one ambiguity in cross-references *(audit finding: "Step 1 not formally numbered in Research Steps section")*
- [ ] **Step 6B Source Priority Table Entry** — add Step 6B (Decision-Maker Dossiers) as a row in the Source Priority Reference table — every step from 2–17 has a row except Step 6B; Checker has no canonical source hierarchy to enforce for this step *(audit finding: "Step 6B absent from Source Priority Reference table")*
- [ ] **Step 10B Dependency Declaration Fix** — update Step 10B preamble from "Depends on: Steps 2–10" to "Depends on: Steps 2–14" — the ICP Score dimensions draw from Step 12 (Social presence) and Step 14 (Growth/change signal), making the current 2–10 declaration factually inaccurate *(audit finding: "Step 10B dependency declaration is incomplete — actually requires Steps 12 and 14")*
- [ ] **Checker Criterion #7 Scope Update** — extend BD Relevance criterion scope to include Steps 16 and 17 (currently only lists Steps 8, 10, 12, 14, 15) — Steps 16 and 17 both have explicit BD framing rules and BD signal output fields that go unenforced *(audit finding: "Steps 16 and 17 have BD framing requirements not covered by Criterion #7 scope")*
- [ ] **Step 15 Dependency Clarification** — change "Synthesize findings from Steps 2–17" to "Synthesize findings from Steps 2–14, 16, and 17" — Step 15 is itself within 2–17, making the current instruction a circular reference *(audit finding: "circular dependency language: Step 15 told to synthesize from a range that includes itself")*
- [ ] **Wave 2 Read-Scope Correction** — update Wave 2 worker read-scope from "Steps 2–9" to "Steps 2–9, 11–14, 16–17" for Step 10B specifically — Step 10B dimensions reference Steps 12 and 14 which are outside the 2–9 range *(audit finding: "Wave 2 read-scope understates Step 10B dependencies")*
- [ ] **Orchestrator Worker Count Annotation** — annotate "19 Workers" in Orchestrator Instructions as "19 = 17 Wave 1 Workers (Steps 2–9, 11–14, 16–17) + 2 Wave 2 Workers (Steps 10 + 10B)" — the unexplained count causes confusion when steps are added or removed *(audit finding: "Orchestrator worker count unexplained")*
- [ ] **Sanitizer Scope Explicit Listing** — change "Scan all approved Wave 1 outputs" to "Scan all approved Wave 1 outputs (Steps 2–9, 11–14, 16–17 — 17 steps total)" — implicit scope requires workers to infer the step list *(audit finding: "Sanitizer scope is implicit — step list never enumerated")*
- [ ] **Platform Execution Mode Table Update** — add Claude Desktop (MCP), Cursor, VS Code Agent, Cline, Continue.dev, and Windsurf to the PARALLEL or SEQUENTIAL column — currently only lists Claude Code, OpenCode, Codex agent (PARALLEL) and Claude.ai, Cowork, Codex chat (SEQUENTIAL) *(audit finding: "table missing named platforms; users on Cursor/VS Code default to SEQUENTIAL incorrectly")*
- [ ] **Tool Absence Degradation Protocol** — add a tool-absence rule to Core Research Principles: "If a required tool class (web search / file write / subagents) is entirely unavailable, halt and notify the user before proceeding" — the current rate-limit protocol does not cover tool-absent environments *(audit finding: "no protocol for when a tool class is entirely absent from the executing environment")*
- [ ] **Compatibility Statement Update** — add Claude Desktop (MCP), Cursor, and VS Code Agent to the "Compatible with" line — the current list (Claude.ai, Claude Code, Cowork, OpenCode, Codex) does not reflect the current platform landscape *(audit finding: "compatibility statement missing Claude Desktop, Cursor, and other modern platforms")*

---