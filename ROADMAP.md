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
