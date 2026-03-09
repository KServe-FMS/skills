---
name: company-research
description: >
  Comprehensive BD intelligence research skill for KServe's business development team.
  Use this skill whenever a user provides a company name (and optionally a website or address)
  and wants to research that company as a potential outsourcing client. Triggers on phrases like
  "research [company]", "look up [company]", "get me info on [company]", "do a BD profile for [company]",
  "check out this company", or any request to investigate a prospect company for sales or outreach purposes.
  Always use this skill when the context is about finding potential clients for KServe's BPO services.
---

# KServe Company Research Skill

This skill produces a comprehensive BD intelligence report on a prospect company so KServe's business development team can reach out to the right people with the right message. The output is a structured chat summary with verified sources for every data point.

**Compatible with:** Claude.ai · Claude Code · Cowork · OpenCode · Codex · Any AI agent platform

---

## About KServe

KServe is an AI-powered Business Process Outsourcing (BPO) company headquartered in Thane, Maharashtra, India. KServe helps businesses grow and operate more efficiently by taking over key business functions — powered by integrated AI technology that delivers faster turnaround, higher accuracy, and better outcomes than traditional BPO.

### Services

| Service | What KServe does |
|---|---|
| **Lead Generation** | Identifies and sources potential customers for the client's sales pipeline |
| **Lead Qualification** | Evaluates leads to determine fit, intent, and readiness to buy — so the client's sales team focuses only on high-value prospects |
| **Customer Onboarding** | Manages the end-to-end process of welcoming and activating new customers on behalf of the client |
| **Staff Augmentation** | Provides trained, dedicated staff who work as an extension of the client's own team — without the overhead of in-house hiring |
| **Customer Service** | Handles inbound and outbound customer interactions across voice, chat, email, and other channels |
| **Back-Office Operations** | Takes over internal processing tasks — data entry, documentation, verification, and admin workflows |
| **Collection** | Manages payment follow-ups, outstanding dues, and recovery processes on behalf of the client |
| **Market Research** | Gathers competitive intelligence, customer insights, and market data to support the client's business decisions |

> All services can be augmented with KServe's AI technology — enabling automation, smarter routing, predictive insights, and higher throughput at lower cost.

### Target Industries

BFSI · NBFC · Banking & Securities · Insurance · eCommerce · Education / EdTech · Automobile · Energy & Utilities · Healthcare · Media & Entertainment · Real Estate · Retail · Manufacturing · Tours & Travel · Hospitality · Agriculture · Immigration · Accounting · Fintech · Food & Beverages · Supply Chain Management · Logistics

---

## Platform Execution Mode

Detect your execution mode before starting. Apply it consistently throughout.

| Mode | When to use | Platforms |
|---|---|---|
| **PARALLEL** | You can spawn independent subagents that run simultaneously | Claude Code (`Task` tool) · OpenCode (`Task`) · Codex agent (`spawn_agent`) · Any multi-agent platform |
| **SEQUENTIAL** | Single-thread only — one step at a time | Claude.ai · Cowork · Codex chat · Any single-thread assistant |

If unsure, default to **SEQUENTIAL** — it is always safe, just slower.

**PARALLEL:** Spawn Workers 2–15 all at once after user confirms. Each Worker runs its own Checker loop. Orchestrator assembles the report once all Workers complete. Note: Step 10 (KServe Fit) depends on Steps 2–9 — spawn it last.

**SEQUENTIAL:** Run Steps 2–15 in order. Complete each Worker → Checker loop before advancing. Assemble and present the full report after Step 15.

Tool naming across platforms:
- Web search: `web_search`, `WebSearch`, `search`, `browse`, or equivalent
- File write: `write_file`, `Write`, `fs.write`, or equivalent
- Subagents: `Task`, `spawn_agent`, `create_agent`, or platform equivalent

---

## Research Flow

### Phase 1 — Verification (always first, on every platform)

Search the web for the company. Present the user with:
- Company name (as found)
- Website URL
- Registered / primary address
- Brief one-line description

**Stop and wait for the user to confirm** this is the right company before proceeding. If the user provided a website or address, use it to narrow the search.

Example:
```
I found the following. Is this the company you mean?

**Name:** Reliance Retail Ltd.
**Website:** https://www.relianceretail.com
**Address:** 3rd Floor, Court House, Lokmanya Bal Gangadhar Tilak Marg, Mumbai – 400002
**About:** India's largest retail chain across grocery, fashion, and electronics.

Please confirm and I'll run the full research.
```

### Phase 2 — Full Research (after user confirms)

Run all 14 research steps (Steps 2–15) using the execution mode detected above. Each step follows the **Worker → Checker → Orchestrator** pattern:

1. **Worker** gathers data for that step using available web/search tools
2. **Checker** validates the output against the five criteria (see Checker Instructions)
3. If anything fails, Checker returns specific feedback to Worker — loop repeats
4. Once approved, output passes to the **Orchestrator**
5. **Orchestrator** assembles the final report once all steps are complete

---

## Core Research Principles

These principles apply to every step and every platform. Read them before executing any step.

**Recency first.** Prioritize sources from the last 12 months. If only older data is available, use it but note in report: `⚠️ Most recent available: [FY/date]. Newer data may not yet be public.`

**Every data point needs a source.** Never present a fact without a URL or document reference. If something cannot be sourced, write "Not publicly available" — do not guess.

**MCA is ground truth for Indian companies.** For these fields, always use MCA (mca.gov.in) as the primary source:
- Incorporation date (Step 5)
- Current directors (Step 6)
- Registered address (Step 4)
- Financial filings / turnover (Step 3)

Tofler, Zauba Corp, and similar aggregators pull from MCA and are acceptable secondary sources.

**BD framing throughout.** Every section must be written with the lens of: *"How does this help KServe win this account?"* — not raw data, but insight.

**Graceful degradation.** If a tool or data source is unavailable, note it clearly in that section and move on. Never halt the entire report because one step hit a wall.

**Zero results = explicit statement.** If a web search returns no results for a required field, write "Not publicly available" or "No results found" in the report. Never fill a gap by inferring from adjacent context, similar companies, or general knowledge. An acknowledged gap is always more trustworthy than an unverified inference — and an incorrect data point handed to BD is actively harmful.

---

## Source Priority Reference

Use this table for every step. Each step lists which sources to try in order of preference.

| Step | Primary | Secondary | Fallback |
|---|---|---|---|
| 2 — Line of Business | Company website (About page) | LinkedIn company page | News articles · Industry directories |
| 3 — Turnover | MCA filings (AOC-4 Annual Return, MGT-7 Board Report) | Tofler · Zauba Corp | News articles · Annual reports |
| 4 — Head Office | MCA registered address | Company website | Google Maps Business listing |
| 5 — Years in Existence | MCA company master data | Company website (Our Story / About) | LinkedIn Founded year · Wikipedia |
| 6 — Directors | MCA director listing | Tofler | Company website (Leadership) · LinkedIn |
| 7 — Branches | Company website | Google Maps | News · LinkedIn (employees by location) |
| 8 — Reviews | Google Business · Glassdoor · AmbitionBox (see step for industry table) | Trustpilot · Justdial · IndiaMart | App Store / Play Store reviews |
| 9 — Rating | Synthesized from Step 8 output | — | — |
| 10 — KServe Fit | Synthesized from Steps 2–9 output | — | — |
| 11 — Customer Care | Company website | Google Business · Justdial | App Store / Play Store listing |
| 12 — Social Media | Direct platform search (LinkedIn, Instagram, Facebook, X, YouTube) | Social Blade (trends) | Company website social links |
| 13 — Tracxn | Tracxn.com | Crunchbase (fallback if Tracxn locked) | — |
| 14 — M&A | News (last 12 months) | Tracxn · Crunchbase · MCA filings | ET · Mint · Business Standard |
| 15 — BD Briefing | Synthesized from Steps 2–14 output — no new searches | — | — |

---

## Research Steps (Steps 2–15)

### Step 2 — Line of Business

Find: industry, core products/services, business model (B2B / B2C / B2G), key customer segments.

---

### Step 3 — Turnover (₹ Crores)

Find annual revenue/turnover in Indian Rupees (Crores). Always include the financial year (e.g., FY2023-24).

For Indian-registered companies: use MCA annual filings → Tofler/Zauba → news.
For non-Indian companies or Indian subsidiaries of foreign entities: report in original currency, convert to INR at filing-date exchange rate, and note in report: `Revenue in [currency]; converted to INR at [rate] as of [date].`
If not publicly available: write "Private company — turnover not publicly disclosed."

---

### Step 4 — Head Office Location

Find the primary registered office address. Cross-reference MCA registered address against company website — they sometimes differ. If different, report both: `Registered (MCA): [address] | Current operations (website): [address]`

---

### Step 5 — Years in Existence

Find the incorporation / founding year. Calculate age from today.

---

### Step 6 — Directors

Pull current directors from MCA. For each: Full name · Designation (MD, Director, Independent Director, etc.) · DIN (Director Identification Number).

For BD outreach, identify for BD outreach: directors likely to be decision-makers for outsourcing (MD, COO, CFO, VP Operations).

---

### Step 7 — Branches & Offices

Find: total number of offices/branches/locations · key cities/states · any international presence.

---

### Step 8 — Reviews & Reputation (Last 12 Months)

Search for reviews from the **last 12 months** on platforms relevant to the company type:

| Company type | Platforms to check |
|---|---|
| Consumer brand / eCommerce | Google Business · Trustpilot · Flipkart · Amazon · Myntra |
| Employer brand | AmbitionBox · Glassdoor · Indeed |
| B2B / General | Google Business · Justdial · IndiaMart |
| Finance / Insurance | Google Business · consumer forums |

Synthesize into:
- **Top 5 Positives** — recurring themes across multiple reviews (note frequency)
- **Top 5 Negatives** — recurring pain points (these are BD opportunities for KServe)
- **Platforms checked** — list each with review count and date range

If less than 12 months of reviews exist, include older reviews and note in report: `⚠️ Full 12-month data unavailable; includes reviews from [date range].`

---

### Step 9 — Overall Business Rating (out of 10)

Assign a synthesized reputation score — NOT an average of star ratings. Base it on the review themes from Step 8.

**Rating anchors:**

| Score | Label | Criteria |
|---|---|---|
| 9–10 | Excellent | Few complaints, strong positive trends, company actively responds to feedback |
| 7–8 | Good | Mostly positive, some recurring but minor issues |
| 5–6 | Fair | Mixed reviews, notable pain points alongside positives |
| 3–4 | Poor | Majority negative, serious issues (e.g., unfulfilled orders, unresolved complaints), low responsiveness |
| 1–2 | Very Poor | Severe, consistent failures across multiple platforms |

Provide a 2–3 sentence rationale. Note: a lower score often signals more BPO opportunity for KServe.

---

### Step 10 — KServe Services Fit

**Depends on:** Steps 2–9 (LoB, size, reviews, directors). In PARALLEL mode, run this step last — after all other workers complete.

Based on the full research picture, recommend **3–5 services** (not all 8) with explicit fit levels:

- ⭐ **HIGH FIT** — service directly addresses a visible pain point found in reviews or news
- ✅ **MEDIUM FIT** — service aligns with company strategy, size, or industry norms

Omit LOW FIT services entirely — only include what is genuinely relevant.

Format each as: `[Service] — [Fit level] — [Specific evidence from research]`

Example:
```
Customer Service ⭐ HIGH FIT
Glassdoor reviews cite "2-hour wait times" and "unresponsive support" — a direct signal
that in-house customer ops are stretched. KServe's AI-powered CX management addresses this.

Lead Generation ✅ MEDIUM FIT
Company is expanding into 3 new cities (per recent news). Qualified outbound lead gen
could accelerate market entry without growing headcount.
```

---

### Step 11 — Customer Care Number

Find their publicly listed customer support / helpline number.

BD insight: presence of a published number signals a formal support structure. Absence may indicate underdeveloped customer ops — a potential KServe entry point. If no number is found, note in report: "No published support number found."

---

### Step 12 — Social Media Followers

Pull current follower counts: LinkedIn · Instagram · Facebook · Twitter/X · YouTube (if applicable).

Engagement signal (check the main platform — LinkedIn for B2B):
- Review last 5–10 posts
- Note if engagement rate appears low (<2% likes+comments/followers) or posting frequency is sparse (<1×/month)
- Flag low engagement in report as: `Low engagement — [platform]: [observation]`

---

### Step 13 — Tracxn Profile

Search Tracxn.com for the company. Report: Tracxn Score (0–100 scale, if available) · category/sector tags · funding stage · investors · notable badges.

If company is not on Tracxn (common for traditional/non-VC companies): note in report `Not on Tracxn — likely private/bootstrapped.` and check Crunchbase as fallback.

If Tracxn profile requires a paid subscription to view detail: note in report `Tracxn profile exists but detail is gated.`

---

### Step 14 — Acquisitions & M&A Activity

Search for any recent (last 12 months preferred): acquisitions · being acquired · mergers · major investment rounds · PE/VC backing changes.

BD signals:
- Being acquired → may freeze vendor decisions (note in report)
- Fresh funding raised → likely expanding, open to outsourcing (highlight as trigger signal for Step 15)

---

### Step 15 — BD Intelligence Briefing

**Most important step.** Synthesize findings from Steps 2–14 into actionable outreach intel. **Do not run new web searches** — use only what was gathered in prior steps.

**A. Things to Know Before Reaching Out** (3–5 bullet points)
Current strategic focus · key decision-makers · recent challenges visible in research.

**B. Conversation Starters** (3–5 specific, recent hooks)
Based on actual events found in research (expansion, funding, product launch, leadership hire, negative reviews).
Format: *"[Company] recently [event] — we've helped similar companies with [KServe service] in situations like this."*

**C. Trigger Signals — Why Reach Out Now** (top 2–3 only)
Select the most compelling from:
- Rapid hiring (scaling pain) · Geographic expansion · New product/service launch
- Negative reviews spiking · Funding round closed · Leadership change

**D. Potential Objections & Responses** (2–3 only)
Based on company profile, anticipate likely pushbacks and provide a suggested KServe response for each.

---

## Output Format

Present the final report using this template:

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
🏢 KSERVE BD RESEARCH REPORT
Company: [Name]
Research Date: [Date]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

✅ VERIFICATION
[Website | Address | Confirmed by user]

📋 LINE OF BUSINESS
[Summary]
Source(s): [URL] | [URL] | Confidence: HIGH/MED/LOW | Source date: YYYY-MM-DD

💰 TURNOVER
[₹ X Crores | FY XXXX-XX]
Source(s): [URL] | Confidence: HIGH/MED/LOW | Source date: YYYY-MM-DD

📍 HEAD OFFICE
[Address]
Source(s): [URL] | Confidence: HIGH/MED/LOW | Source date: YYYY-MM-DD

📅 YEARS IN EXISTENCE
[Founded XXXX | X years old]
Source(s): [URL] | Confidence: HIGH/MED/LOW | Source date: YYYY-MM-DD

👔 DIRECTORS
[Name — Designation — DIN]
[Name — Designation — DIN]
Source(s): [MCA URL] | Confidence: HIGH/MED/LOW | Source date: YYYY-MM-DD

🗺️ BRANCHES & OFFICES
[X locations | Key cities]
Source(s): [URL] | Confidence: HIGH/MED/LOW | Source date: YYYY-MM-DD

⭐ REVIEWS & REPUTATION (Last 12 months)
Top 5 Positives:
1. ...
Top 5 Negatives:
1. ...
Platforms checked: [Platform — X reviews — date range — URL]
Confidence: HIGH/MED/LOW | Most recent review: YYYY-MM-DD

🎯 OVERALL RATING: X/10 — [Label]
[2–3 sentence rationale]

🤝 KSERVE FIT ASSESSMENT
[Service — Fit level — Evidence]

📞 CUSTOMER CARE NUMBER
[Number or "Not published"] | Source(s): [URL] | Confidence: HIGH/MED/LOW | Source date: YYYY-MM-DD

📱 SOCIAL MEDIA FOLLOWERS
LinkedIn: X | Instagram: X | Facebook: X | Twitter/X: X | YouTube: X
Source(s): [URLs] | Confidence: HIGH/MED/LOW | Checked: YYYY-MM-DD

📊 TRACXN PROFILE
[Score / Not listed / Gated]
Source(s): [URL] | Confidence: HIGH/MED/LOW | Source date: YYYY-MM-DD

🔀 M&A & FUNDING ACTIVITY
[Summary or "No recent M&A activity found"]
Source(s): [URL] | Confidence: HIGH/MED/LOW | Source date: YYYY-MM-DD

🧠 BD INTELLIGENCE BRIEFING

Things to Know:
• ...

Conversation Starters:
• ...

Trigger Signals:
• ...

Potential Objections:
• [Objection] → [Suggested response]

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
📝 DATA QUALITY
Overall: [e.g., 9/14 fields HIGH · 3 MED · 2 LOW]
Data gaps: [List any fields that hit retry limit, or "None"]
Oldest source: [YYYY-MM-DD]

Confidence key: HIGH = MCA-verified or 2+ independent sources · MED = single credible source or aggregator · LOW = estimated, partial, or unverified
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

---

## Multi-Agent Architecture

### PARALLEL MODE

```
User confirms company (Step 1)
         │
         ▼
┌─────────────────────────────────────────┐
│    SPAWN SIMULTANEOUSLY (Steps 2–9, 11–14)   │
│  Worker-2   Worker-3   Worker-4  ...    │
│  Worker-5   Worker-6   Worker-7  ...    │
│  Worker-8   Worker-9   Worker-11 ...    │
│  Worker-12  Worker-13  Worker-14        │
│  (Step 10 spawns last — needs 2–9)      │
└─────────────────────────────────────────┘
         │ (each worker ↔ checker loop)
         ▼
┌─────────────────────────────────────────┐
│      CHECKER (per worker)               │
│  Validates: source · credibility ·      │
│  recency · accuracy · completeness      │
│  Returns to worker if any fail          │
└─────────────────────────────────────────┘
         │ (all approved outputs)
         ▼
┌─────────────────────────────────────────┐
│         ORCHESTRATOR                    │
│  Assembles all 14 approved sections     │
│  Validates completeness of report       │
│  Renders final BD Research Report       │
└─────────────────────────────────────────┘
```

### SEQUENTIAL MODE

```
User confirms company (Step 1)
         │
    ┌────▼────┐
    │ Step 2  │ Worker → Checker validates → approved ✓
    └────┬────┘
    ┌────▼────┐
    │ Step 3  │ Worker → Checker validates → approved ✓
    └────┬────┘
        ...
    ┌────▼─────┐
    │ Step 15  │ Worker → Checker validates → approved ✓
    └────┬─────┘
         │
         ▼
  Orchestrator assembles and presents final report
```

---

## Checker Instructions

When validating any Worker output, apply all five criteria:

1. **Source present?** Every fact must have a URL or named document. No source → send back.
2. **Source credible?** Prefer official sources (MCA, company website, major publications) over anonymous forums or low-quality aggregators.
3. **Recency?** Is the data from the last 12 months? If older, is it noted in the report with a ⚠️?
4. **Accurate?** Does the data make internal sense? (e.g., a 2-year-old company cannot have 50 years of history)
5. **Complete?** Did the Worker answer everything the step requires, or are there gaps?
6. **Source diversity?** For high-stakes fields (Turnover, Directors, Head Office, Years in Existence), are there at least 2 *independent* sources? Two aggregators that both pull from MCA (e.g., Tofler + Zauba Corp) do not count as independent — MCA is the single source. If only one source exists, the field must be marked `Confidence: MED` or `LOW`, not `HIGH`. This isn't a blocker — it's a signal for the output.
7. **BD relevance?** Does this output answer *"why should KServe reach out to this company now?"* — not just what is factually true, but what is strategically actionable. A section that lists accurate data with no BD framing should be sent back: *"Add a BD insight — what does this data signal for KServe's outreach opportunity?"* This criterion applies most strictly to Steps 8, 10, 12, 14, and 15.

If any criterion fails, return to Worker with specific, actionable feedback:
*"The turnover figure has no source — find the MCA filing or a news article citing the exact revenue figure."*

**Max retries: 2.** If the Worker cannot satisfy all criteria after 2 attempts, it must send this structured signal to the Orchestrator before approving:

`RETRY_EXHAUSTED: [Step N] — [field name] — [reason data is incomplete or unavailable]`

Then approve the best available output with this note in the report:
`⚠️ [Field]: Best available data — [brief reason]`

The Orchestrator collects all `RETRY_EXHAUSTED` signals and surfaces them in the Data Quality footer.

**Conflicting sources:** If sources disagree, defer to the most authoritative source using this hierarchy: MCA > official company website > major publications > aggregators. Report all versions with source label.

**Common contradiction patterns to check proactively:**
- Turnover figures that differ across sources — verify the financial year and entity (parent vs. subsidiary) before flagging
- Director names on MCA that differ from company website — recent appointments may not have propagated to MCA yet; report both and note the lag
- Founded year vs. MCA incorporation date — these legitimately differ (founding vs. legal registration); report both if they differ
- Branch count from website vs. Google Maps vs. LinkedIn employees by location — triangulate and report the range if inconsistent

Only approve when all seven criteria are met (or a ⚠️ note and/or `RETRY_EXHAUSTED` signal is included for genuinely unavailable data).

---

## Orchestrator Instructions

After all 14 Workers complete and each Checker has approved:

1. Assemble all approved sections into the Output Format template in order
2. Validate: no field is blank, pending, or "TBD" without a "Not publicly available" statement or a ⚠️ flag
3. If any section is missing or incomplete, return to that step's Checker with a re-request before rendering
4. Collect all `RETRY_EXHAUSTED` signals received from Checkers. If any exist, populate the "Data gaps" line in the 📝 DATA QUALITY footer with: `[Step N — field] — [reason]` for each one. If none, write "None".
5. Tally confidence levels across all 14 sections and populate the "Overall" line in the DATA QUALITY footer (e.g., `9/14 HIGH · 3 MED · 2 LOW`). Find the oldest source date across all sections and populate "Oldest source".
6. Render the final report for presentation to the user
