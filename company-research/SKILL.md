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
| 8 — Reviews | Google Business · Trustpilot · AmbitionBox · Glassdoor | Amazon · Flipkart · App Store · Google Play · Justdial | AppFollow · AppBot (app reviews) · job postings (Step 8E tool detection only) |
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

Research all five sub-sections below. Each sub-section is mandatory — if no data is found for a sub-section, state that explicitly (e.g., "No product reviews found on searched platforms"). Do not silently omit any sub-section.

If less than 12 months of reviews exist for any sub-section, include older reviews and note: `⚠️ Full 12-month data unavailable; includes reviews from [date range].`

---

**A — Product Review**

Search for product-specific reviews and, if the company has a consumer app, app store reviews.

Product review sources (use platforms relevant to the company type):

| Company type | Platforms |
|---|---|
| Consumer brand / eCommerce | Amazon · Flipkart · Myntra · Google Shopping |
| SaaS / B2B software | G2 · Capterra · Software Advice |
| Finance / Insurance | consumer forums · Google Business product listings |
| General | IndiaMart · Justdial product listings |

App review sources:
1. Primary — direct search: `site:apps.apple.com [company name]` and `site:play.google.com [company name]`
2. Secondary — AppFollow.io, AppBot.co (often accessible without paywall)
3. Fallback — Reddit, Product Hunt, tech blogs

Find:
- Platform, aggregate rating, review volume
- Top recurring themes from critical reviews (1–2 stars): note the most frequent complaints, platforms, and date range
- Top recurring themes from positive reviews (4–5 stars): same format
- For apps: app name, platform (iOS / Android / Both), aggregate rating; any visible company replies on reviews — quote verbatim ≤40 words, note whether replies appear on positive, negative, or both reviews
- If no app found: write `No consumer app found — app review not applicable` and document the search query used
- If app found but reviews are gated: write `App found ([name] — [rating]/5 on [platform]) but individual review content is gated`

BD framing: what does product/app quality feedback signal about operational gaps KServe can address?

---

**B — Service Review**

Search for customer sentiment about how the company serves its customers — support quality, delivery, responsiveness, experience.

Sources:
- Google Business Profile, Trustpilot, Justdial (all company types)
- Finance / Insurance: banking ombudsman forums, consumer court portals, RBI complaint trackers
- B2B: IndiaMart seller ratings, LinkedIn client testimonials, absence of case studies as a signal

Find:
- Recurring themes in customer service feedback: response time, resolution quality, staff attitude
- Specific complaints about support channels (phone, chat, email, in-store)
- Platforms checked with review count and date range

BD framing: where does customer service break down? This maps directly to KServe's Customer Service offering.

---

**C — Employee Review**

Search for what employees say about working at this company — signals operational maturity, management culture, and attrition risk.

Sources:
- AmbitionBox (primary for Indian companies), Glassdoor, Indeed
- LinkedIn "Reviews" tab if available

Find:
- Overall rating on each platform, review volume
- Top 3 positives (recurring themes)
- Top 3 negatives (recurring themes)
- Any mentions of process quality, training programs, tech stack, attrition rate, management style

BD framing: high attrition or poor internal process = outsourcing appetite; strong culture = partnership-friendly decision-maker.

---

**D — General Company Review**

Search for overall public perception, business reputation, and press sentiment — the narrative that doesn't fit product or service reviews.

Sources:
- Google Business (overall company rating, not product/service-specific)
- Industry forums and discussion boards
- News and media sentiment (last 12 months)
- Justdial, IndiaMart general business listings

Find:
- Overall public reputation narrative
- Any controversies, regulatory issues, or legal disputes
- Any awards, recognitions, or positive press
- Key sentiment trend (improving / stable / declining)

BD framing: reputational context that shapes outreach tone — a company under scrutiny needs a different pitch than one riding a growth wave.

---

**E — Review Handling Methodology**

Research how the company manages and responds to reviews across all platforms found in A–D. Use what was already observed in A–D as your primary signal. Run targeted additional searches only for tool detection (job postings, BuiltWith) — do not re-research review content already gathered.

Look for evidence of:

| Signal | Where to find it |
|---|---|
| Platform-native replies | Replies visible on Google Maps, App Store, Play Store, Trustpilot, Glassdoor |
| Email-based follow-up | Company support/FAQ pages; reviewer mentions ("they emailed me after I posted") |
| Third-party review tools | Job postings: `[company] "Birdeye" OR "Yotpo" OR "Respond.io" OR "Medallia" OR "ReviewTrackers"`; BuiltWith / G2 integrations |
| Automated vs manual | Identical boilerplate across reviews = likely automated; named agent sign-off + review-specific language = manual |
| Response rate | From reviews examined: High (>60%) / Medium (20–60%) / Low (<20%) / None — always note sample size (e.g., "based on 12 reviews examined") |
| Response speed | Timestamp lag between review and reply: <24h / 1–7 days / >7 days / Inconsistent / Not determinable |

Synthesize into:
- Response channel(s) used
- Response style: Personalized / Templated / Mixed / Not found
- Response rate estimate with basis
- Response speed estimate
- Tool indicators (any third-party review management tools detected)
- **BD signal**: what does this methodology reveal about the company's CS culture, and where does KServe's offering address the gap? Must be an implication, not a description ("They respond to reviews" is not BD insight).

If no responses found across any platform: `No review responses found across [list platforms checked] — no active review management program detected, or handling is off-platform (email/DM only).`

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

If Step 8E found response rate Low or None: include a bullet noting the visible CS gap — list platforms checked and the estimated response rate. If Step 8A found an app rating below 3.5/5 with meaningful review volume: include a bullet on the app reputation risk and whether the company is actively engaging with it.

**B. Conversation Starters** (3–5 specific, recent hooks)
Based on actual events found in research (expansion, funding, product launch, leadership hire, negative reviews).
Format: *"[Company] recently [event] — we've helped similar companies with [KServe service] in situations like this."*

If Step 8E found templated or absent review responses, use: *"[Company] has [X] reviews on [platform] with a [High/Medium/Low/None] reply rate — we've helped similar [industry] companies set up structured review response programs as part of a broader CX operation."* Use only if evidenced in Step 8E — do not fabricate reply-rate label or platform details.

**C. Trigger Signals — Why Reach Out Now** (top 2–3 only)
Select the most compelling from:
- Rapid hiring (scaling pain) · Geographic expansion · New product/service launch
- Negative reviews spiking · Funding round closed · Leadership change
- App store rating below 3.5/5 with high review volume → visible product/service quality signal
- Review response rate Low or None across multiple platforms → underdeveloped CS infrastructure
- Third-party review tool detected (e.g., Birdeye, Yotpo) → pitch shifts from "you need this" to "we can operate this for you at scale"

**D. Potential Objections & Responses** (2–3 only)
Based on company profile, anticipate likely pushbacks and provide a suggested KServe response for each.

If a review management tool was detected in Step 8E, anticipate: *"We already use [tool] to manage reviews."* Suggested response: *"That's exactly the setup we integrate with — KServe handles the human judgment layer (response drafting, escalation routing) within your existing tool. You keep the tech stack, we remove the headcount burden."*

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

📦 A — PRODUCT REVIEW
[If no product reviews found: "No product reviews found on searched platforms"]
Platform — Rating — Review count — URL
Top critical themes: ...
Top positive themes: ...
App:
  [Found]: [name] | [iOS / Android / Both] | [X.X]/5 ([X,XXX] ratings)
    Sample critical: "[verbatim ≤40 words]" — [reviewer] — [YYYY-MM-DD] | [URL]
    Sample positive: "[verbatim ≤40 words]" — [reviewer] — [YYYY-MM-DD] | [URL]
    Company replies on app: Yes / No / Partial
  [Not found]: "No consumer app found — app review not applicable. Search query used: [query]"
Confidence: HIGH/MED/LOW | Most recent: YYYY-MM-DD

🛎️ B — SERVICE REVIEW
[If no service reviews found: "No service reviews found on searched platforms"]
Platform — Rating — Review count — URL
Top positives: ...
Top negatives: ...
Notable signal: [e.g., "No case studies found — signals limited B2B social proof" / "N/A"]
BD signal: [what this means for KServe's Customer Service pitch]
Confidence: HIGH/MED/LOW | Most recent: YYYY-MM-DD

👥 C — EMPLOYEE REVIEW
[If no employee reviews found: "No employee reviews found on searched platforms"]
Platform — Rating — Review count — URL
Top positives: ...
Top negatives: ...
BD signal: [attrition / culture signal for outreach approach]
Confidence: HIGH/MED/LOW | Most recent: YYYY-MM-DD

🌐 D — GENERAL COMPANY REVIEW
[If no general reviews found: "No general company reviews found on searched platforms"]
Platform — Rating — URL
Overall reputation narrative: ...
Notable: [awards / controversies / press sentiment]
Confidence: HIGH/MED/LOW | Most recent: YYYY-MM-DD

🔄 E — REVIEW HANDLING METHODOLOGY
Response channel(s): [e.g., Google Maps native · App Store native / Not found]
Response style: Personalized / Templated / Mixed / Not found
Response rate: High (>60%) / Medium (20–60%) / Low (<20%) / None [sample: X reviews examined]
Response speed: <24h / 1–7 days / >7 days / Inconsistent / Not determinable
Tool indicators: [e.g., "Job posting cites Birdeye" / "None detected"]
BD signal: [1–2 sentences: CS culture implication and KServe opportunity]
Source(s): [URL] | Confidence: HIGH/MED/LOW | Source date: YYYY-MM-DD

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

   *For Step 8 specifically:* Did the Worker produce all five sub-sections (A — Product Review, B — Service Review, C — Employee Review, D — General Company Review, E — Review Handling Methodology)? Sub-sections are not optional — if a sub-section has no data, it must say so explicitly (e.g., "No product reviews found"). Silent omissions → send back. Verbatim review excerpts (required in Section A only; B, C, and D use themes — not quotes) must be: in quotation marks, ≤40 words, attributed with date and source URL. Paraphrases dressed as quotes → send back.

6. **Source diversity?** For high-stakes fields (Turnover, Directors, Head Office, Years in Existence), are there at least 2 *independent* sources? Two aggregators that both pull from MCA (e.g., Tofler + Zauba Corp) do not count as independent — MCA is the single source. If only one source exists, the field must be marked `Confidence: MED` or `LOW`, not `HIGH`. This isn't a blocker — it's a signal for the output.
7. **BD relevance?** Does this output answer *"why should KServe reach out to this company now?"* — not just what is factually true, but what is strategically actionable. A section that lists accurate data with no BD framing should be sent back: *"Add a BD insight — what does this data signal for KServe's outreach opportunity?"* This criterion applies most strictly to Steps 8, 10, 12, 14, and 15.

   *For Step 8E specifically:* The BD signal field must be an implication, not a description. "They respond to reviews" is not BD insight. Acceptable example: "Review responses are boilerplate and slow (>7 days) — signals understaffed or unstructured CS; KServe's Customer Service offering directly addresses this." If the BD signal reads as description only → send back. Response rate estimates must always reference a sample count (e.g., "based on 12 reviews examined") — not conditional on volume. "None detected" is always valid if platforms were checked. Section 8E defaults to Confidence: MED (methodology is inferred, not stated) unless a job posting or news article explicitly names a tool or process.

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
