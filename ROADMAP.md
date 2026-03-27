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
- [ ] **ESG / Sustainability Signals** — check for CSR filings (MCA Schedule VII), sustainability reports, and BRSR disclosures for listed companies — ESG-committed companies face higher compliance documentation load, a direct KServe back-office opportunity

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
- [ ] **GeM Supplier Profile Depth** — extend Step 14 GeM check with bid history, active tenders, and awarded contract values — government contract volume signals compliance maturity and procurement cycle length, both of which shape the KServe pitch approach

### India-Primary Additions
- [ ] **GST Registration & Compliance Status** — search the GSTIN database for registration status, return-filing compliance, and any cancellation or suspension notices — GST non-compliance signals working capital stress and is an outsourcing receptivity trigger
- [ ] **EPFO Filing Signals** — cross-reference EPFO monthly employer ECR filings to triangulate actual headcount independent of LinkedIn estimates — more reliable for blue-collar-heavy industries where LinkedIn employee counts are systematically understated
- [ ] **CIBIL / Credit Bureau Risk Flag** — search for public CIBIL defaulter mentions, RBI NPA classification, or SARFAESI action — high credit risk is a distress signal that makes cost-reduction pitches (KServe's collections and back-office) immediately relevant
- [ ] **eCourts & NCLAT Case Search** — search eCourts India for active civil/commercial cases and NCLAT for insolvency/winding-up proceedings — active litigation signals operational stress and may indicate a freeze on new vendor commitments
- [ ] **Startup India / DPIIT Recognition Status** — check DPIIT startup recognition certificate status — recognized startups get regulatory relaxations and disproportionately need scale-without-headcount solutions that KServe provides
- [ ] **SEBI Listed Entity Depth** — for BSE/NSE-listed companies, pull shareholding pattern, promoter pledge percentage, and quarterly results trend — promoter pledge above 50% is a financial stress indicator that elevates outsourcing receptivity
- [ ] **CIN-Level Subsidiary & Group Mapping** — search MCA for all entities sharing the same promoter DIN to reveal group company structure — group presence expands the total addressable relationship: win one entity, pitch the group
- [ ] **Regional Language Review Mining** — search for reviews on Sharechat, Koo, regional Facebook groups (Hindi/Marathi/Tamil/Telugu), and local forums — captures sentiment invisible on English-only platforms, especially relevant for tier-2/3 city brands
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
