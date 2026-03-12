# Company Research Skill — Enterprise Roadmap

Checklist of improvements to elevate the skill to enterprise grade. Items are grouped by theme and roughly ordered by impact within each group.

---

## Phase 1 — Research Coverage

### New Data Modules (new steps)
- [ ] **Employee Headcount & Growth Trend** — LinkedIn `#employees` over time; signals scaling pain or hiring freeze
- [x] **Technology Stack Detection** — BuiltWith/Wappalyzer + job postings to detect CRMs, ERPs, cloud providers; reveals digital maturity and integration opportunities *(shipped: Step 7C)*
- [ ] **Current Outsourcing Vendors** — detect competitors already embedded via news/announcements; changes the pitch angle entirely
- [x] **Job Postings as Intent Signals** — live roles on Naukri/LinkedIn reveal what they're hiring vs. what KServe could replace or augment *(shipped: Step 7B)*
- [ ] **Regulatory & Legal Risk** — MCA compliance defaults, consumer court cases, SEBI/RBI notices; distress is both risk and opportunity
- [ ] **Competitive Landscape** — top 3 competitors; positions KServe to cite relevant case studies
- [ ] **Key Partnerships & Integrations** — strategic alliances signal direction and potential entry points
- [ ] **Import/Export Data** — Zauba/Volza trade activity; relevant for logistics and supply chain verticals

### Depth Improvements to Existing Steps
- [x] **Step 6 — Directors** — add LinkedIn profile URLs, tenure, career history, and public quotes; currently only static MCA data *(shipped: Enhancement 2.1 + Step 6B)*
- [x] **Step 8 — Reviews** — add sentiment trend over time (improving or worsening?), not just themes; a worsening trend is a stronger trigger signal *(shipped: Enhancement 2.3)*
- [ ] **Step 12 — Social Media** — add posting frequency trend, content themes, and paid ad activity via Facebook Ad Library
- [x] **Step 13 — Tracxn** — add Crunchbase employee count, funding timeline, and investor tier classification; currently too shallow *(shipped: Enhancement 2.4)*
- [x] **Step 14 — M&A** — extend to government contracts/tenders (GEM portal) and PE ownership structure *(shipped: Enhancement 2.5)*

---

## Phase 2 — BD Intelligence

- [x] **ICP Scoring** — quantified Ideal Customer Profile score (1–100) combining company size, industry match, pain points, growth signals, and tech maturity; gives BD a ranked priority list *(shipped: Step 10B)*
- [x] **Account Tiering** — classify as Tier 1 / 2 / 3 with explicit criteria so BD knows whether to assign a senior AE or an SDR *(shipped: Step 10B tier thresholds)*
- [ ] **Deal Size Estimation** — estimate outsourcing contract value range based on headcount, revenue, and service fit; helps BD prioritize pipeline
- [ ] **BANT Pre-qualification** — Budget (revenue/funding), Authority (director mapping), Need (pain points/jobs), Timeline (growth events); structured for CRM entry
- [x] **Decision-Maker Dossiers** — for each BD-relevant director, a 3-line brief: background, LinkedIn activity pattern, likely objection *(shipped: Step 6B)*
- [ ] **Personalized Outreach Templates** — one email draft per top decision-maker using research findings as hooks, not generic copy
- [ ] **Competitive Positioning** — if they already use a competitor BPO, provide differentiation angle; currently the skill ignores competitive context
- [ ] **Expanded Objection Bank** — Step 15D caps at 2–3; extend to cover cost, trust, data security, cultural fit, and incumbent vendor loyalty
- [x] **Next Best Action** — a single ranked recommendation at the top of the report synthesizing all research into one concrete action (e.g., "Call the COO first — 3 open CX JDs on Naukri") *(shipped: Step 15E)*

---

## Phase 3 — Data Quality & Validation ✅ COMPLETE (shipped in v1.0.2 — 2026-03-09)

- [x] **Per-Field Confidence Scoring** — replace single overall confidence level with per-field scores (e.g., `Turnover: HIGH [MCA-verified]`, `Headcount: LOW [LinkedIn estimate]`)
- [x] **Per-Field Freshness Timestamps** — each data point carries its source date, not just a report-level "data age" summary
- [x] **Source Diversity Enforcement** — Checker flags over-reliance on a single aggregator; require at least 2 independent sources for high-confidence fields
- [x] **Contradiction Detection Protocol** — explicit logic for revenue contradictions across sources, director mismatches, date inconsistencies; beyond current MCA vs. website address case
- [x] **6th Checker Criterion: BD Relevance** — "Does this output answer: *why should KServe reach out NOW?*"; prevents technically complete but strategically empty sections from passing
- [x] **Anti-Hallucination Guardrail** — explicit instruction: if search returns zero results, Worker must state "No results found" — not infer from context
- [x] **Retry Budget Surface** — when a Worker exhausts its 2-retry limit, the Orchestrator must receive and flag that exhaustion explicitly in the final report

---

## Phase 4 — Workflow & Architecture

- [ ] **Batch Mode** — research a list of companies (CSV/list input) in a single invocation, one report per company; critical for vertical campaign execution
- [ ] **Refresh/Delta Mode** — re-research a previously profiled company, surfacing only what changed since the last report
- [ ] **Watchlist/Monitor Mode** — periodically re-check a shortlisted prospect for trigger events (funding, leadership change, bad press spike)
- [x] **Streaming Partial Delivery** — in SEQUENTIAL mode, present each completed section immediately rather than buffering until all steps finish *(shipped: Enhancement 2.8)*
- [x] **Formal Dependency Graph** — declare a DAG for PARALLEL mode; explicit two-wave spawning enforces Step 10/10B dependency *(shipped: Fix 1.2 + Orchestrator validation step)*
- [x] **Live Progress Reporting** — in PARALLEL mode, a status board after Wave 1 spawn; per-step ✓ updates as Workers complete *(shipped: Enhancement 2.7)*
- [ ] **Tool Availability Detection** — if primary search tool is unavailable, explicitly try secondary, then note gap; prevents silent failures
- [x] **Rate Limit Awareness** — detect 429/throttle responses from Tracxn and LinkedIn; switch sources immediately rather than retrying the same endpoint *(shipped: Enhancement 2.6)*
- [x] **Graceful Partial Report** — if 4+ steps fail, Step 15 opens with a partial-data warning header *(shipped: Fix 1.4)*

---

## Phase 5 — Output & Delivery

- [ ] **CRM-Ready JSON Export** — structured JSON block alongside the markdown report with field-mapped data ready for Salesforce/HubSpot import
- [ ] **Executive 1-Pager** — condensed output variant (≤300 words) for leadership review; single prioritized synthesis
- [ ] **Campaign Pitch Brief** — templated output optimized for cold outreach sequencing: Subject line → Hook → Proof point → CTA
- [ ] **Risk Flag Section** — explicit consolidated flags: acquisition freeze signal, regulatory risk, review spike; currently buried in individual step outputs
- [ ] **Audit Trail** — log each source URL, timestamp, and which step consumed it; enables compliance review and source traceability

---

## Phase 6 — Platform & Integration

- [ ] **CRM Record Creation** — post-research, offer to create a CRM record via API (Salesforce/HubSpot)
- [ ] **Slack/Email Delivery** — send completed report to a team channel or BD rep's inbox; useful for async/batch research runs
- [ ] **Multi-Language Output** — generate the BD briefing section in the prospect's primary business language alongside English for international prospects

---

**Total items: 46**
