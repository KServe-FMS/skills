---
name: kserve-company-research
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

## About KServe

KServe is an AI-powered BPO company based in Thane, Maharashtra, India. Services offered:
- Customer Experience Management (multi-channel, multilingual)
- Lead Generation & Qualification
- Back Office Processing & Research
- Finance & Accounting Outsourcing
- Digital Transformation
- Robotic Process Automation (RPA)

Target industries: BFSI, eCommerce, Education/EdTech, Automobile, Energy & Utilities, Healthcare, Media & Entertainment, Real Estate, Retail, Manufacturing.

---

## Research Flow

### Phase 1 — Verification (always first)

Search the web for the company. Present the user with:
- Company name (as found)
- Website URL
- Registered / primary address
- Brief one-line description

Then **stop and wait for the user to confirm** this is the right company before proceeding. If the user provided a website or address alongside the company name, use that to narrow the search.

Example verification message:
```
I found the following. Is this the company you mean?

**Name:** Reliance Retail Ltd.
**Website:** https://www.relianceretail.com
**Address:** 3rd Floor, Court House, Lokmanya Bal Gangadhar Tilak Marg, Dhobi Talao, Mumbai – 400002
**About:** India's largest retail chain operating across grocery, fashion, electronics and more.

Please confirm and I'll run the full research.
```

---

### Phase 2 — Full Research (after user confirms)

Once confirmed, run all 14 research steps. In Claude Code (with subagents), spawn all 14 worker agents simultaneously for maximum speed. On Claude.ai, run them sequentially in order.

Each step follows the **Worker → Checker → Main** pattern:
1. **Worker Agent** gathers data for that specific step
2. **Checker Agent** reviews the output — checks for accuracy, source quality, and freshness. If anything is wrong or unsourced, it sends back to the Worker with specific feedback
3. This loop repeats until Checker approves
4. Approved output is handed to the **Main/Orchestrator Agent** which assembles the final report

---

## Research Steps (Steps 2–15)

### Step 2 — Line of Business
Find what the company actually does: their industry, core products or services, business model (B2B/B2C/B2G), and key customer segments. Go beyond their homepage — look for their "About" page, news coverage, and LinkedIn company description for a grounded picture.

**Source priority:** Company website → LinkedIn → News articles → Industry directories

---

### Step 3 — Turnover (₹ Crores)
Find annual revenue / turnover in Indian Rupees (Crores). For Indian companies, pull from:
1. **MCA (Ministry of Corporate Affairs)** — search https://www.mca.gov.in for the company's annual filings (AOC-4, MGT-7)
2. **Tofler / Zauba Corp / Tracxn** — aggregators of MCA data
3. News articles, annual reports, press releases

Always state the financial year the turnover refers to (e.g., FY2023-24). If only older data is available, flag it clearly: *"Latest available: FY2022-23 — more recent filings not yet public."*

---

### Step 4 — Head Office Location
Find the primary / registered office address. Cross-reference the company website with MCA registered address (they sometimes differ). Note both if different.

**Source priority:** MCA registered address → Company website → Google Maps Business listing

---

### Step 5 — Years in Existence
Find the incorporation / founding year. Calculate age from today. For Indian companies, MCA shows the Date of Incorporation on the company master data page.

**Source priority:** MCA company master data → Company website "Our Story" / "About" → LinkedIn Founded year → News/Wikipedia

---

### Step 6 — Directors
Pull the names and designations of current directors from MCA. Include:
- Full name
- Designation (Managing Director, Director, Independent Director etc.)
- DIN (Director Identification Number) if available — useful for cross-referencing

For BD purposes, flag which directors are likely decision-makers for outsourcing (e.g., COO, CFO, MD, VP Operations).

**Source priority:** MCA → Tofler → Company website Leadership page → LinkedIn

---

### Step 7 — Branches & Offices
Find the number of offices, branches, warehouses, or locations. Include:
- Total count
- Key cities / states
- Any international presence

This matters for KServe because multi-location companies often have distributed customer operations that benefit from centralized BPO support.

**Source priority:** Company website → Google Maps → News → LinkedIn (employees by location filter)

---

### Step 8 — Reviews & Reputation (last 1 year)
Search for reviews across all relevant platforms from the **last 12 months**. Choose platforms based on their industry:

| Company type | Platforms to check |
|---|---|
| Consumer brand / eCommerce | Google Business, Trustpilot, Flipkart, Amazon, Myntra |
| Employer brand | AmbitionBox, Glassdoor, Indeed |
| B2B / General | Google Business, Justdial, IndiaMart |
| Finance / Insurance | Google Business, consumer forums |

Synthesize into:
- **Top 5 Positives** — recurring themes in good reviews
- **Top 5 Negatives** — recurring pain points (these are BD opportunities for KServe!)
- **Platforms checked** with number of reviews found and date range

Always cite source URLs. If less than 12 months of reviews exist, include older reviews and flag it.

---

### Step 9 — Overall Business Rating (out of 10)
Based on the review data from Step 8, assign an overall business health / reputation score out of 10. This is a synthesized judgment, not an average of star ratings.

Consider:
- Consistency of complaints vs. praise
- Severity of negative themes (e.g., "slow delivery" vs. "never received order")
- Volume of reviews and recency
- Response rate of the company to reviews

Provide a **brief rationale** (2–3 sentences) explaining the score. This score is KServe's internal signal — a lower score often means more BPO opportunity.

---

### Step 10 — KServe Services Fit
Based on everything gathered so far (industry, size, reviews, operations), recommend which KServe services would be most relevant to this prospect and why.

Frame this as a BD pitch rationale — not just a list, but a reason:

Example format:
```
**Customer Experience Management** ⭐ High fit
Their Glassdoor reviews mention high call volumes and long wait times — a strong signal
that their in-house customer support is stretched. KServe's CX management with AI-first
tools could directly address this.

**Lead Qualification** ✅ Medium fit
They're expanding into 3 new cities (per recent news). A qualified outbound lead gen
team could accelerate market entry.
```

---

### Step 11 — Customer Care Number
Find their publicly listed customer support / helpline number. This is useful to:
- Understand how they currently handle customer service
- Use as a conversation opener ("We noticed your current support line...")

**Source priority:** Company website → Google Business listing → Justdial → App Store / Play Store listing

---

### Step 12 — Social Media Followers
Pull current follower counts across major platforms:
- LinkedIn (most important for B2B)
- Instagram
- Facebook
- Twitter / X
- YouTube (if applicable)

Note the engagement level if visible (likes per post vs. followers — a large following with low engagement signals a struggling brand).

**Source priority:** Direct platform search → Social Blade (for trends) → Company website social links

---

### Step 13 — Tracxn Score
Search Tracxn (https://tracxn.com) for the company's profile. Report:
- Tracxn Score (if available)
- Tracxn's category / sector tags
- Funding stage and investors (if startup/growth stage)
- Any notable Tracxn badges or rankings

If the company is not on Tracxn (common for traditional/non-VC companies), state this clearly and note it's likely a bootstrapped or unlisted entity.

---

### Step 14 — Acquisitions & M&A Activity
Search for any recent or upcoming:
- Acquisitions (companies they have bought)
- Being acquired (someone buying them)
- Mergers
- Major investment rounds
- PE/VC backing changes

This matters for BD because: a company being acquired may freeze vendor decisions; a company that just raised funding is likely to expand and outsource. M&A activity also reveals strategic direction.

**Source priority:** News (last 12 months preferred) → Tracxn → Crunchbase → MCA filings → Economic Times / Mint / Business Standard

---

### Step 15 — BD Intelligence Briefing
This is the most important step — it turns all the research into actionable intelligence for the person making the first call or sending the first email.

Scan all web articles, press releases, interviews, leadership quotes, job postings, and news mentions. Then produce:

**A. Things to know before reaching out**
Key facts about the company's current state, strategy, and challenges that a BD person must know to have a credible conversation.

**B. Conversation starters**
3–5 specific, relevant openers based on actual recent events. These should feel natural, not salesy. Examples: referencing a recent expansion, a product launch, a leadership hire, or a challenge visible in reviews.

**C. Trigger signals**
Specific events that make NOW a good time for KServe to reach out:
- Rapid hiring (scaling pain)
- Geographic expansion (new markets to support)
- New product/service launch (need for customer support ramp-up)
- Negative reviews spiking (CX problems)
- Funding round (growth capital ready to deploy)
- Leadership change (new decision-makers open to new vendors)

**D. Potential objections & how to handle them**
Based on what you found, anticipate 2–3 likely pushbacks and suggest responses.

---

## Output Format

Present the final report as a structured chat summary using this template:

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
🏢 KSERVE BD RESEARCH REPORT
Company: [Name]
Research Date: [Date]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

✅ VERIFICATION
[Website | Address | Confirmed by user]

📋 LINE OF BUSINESS
[Summary] | Source: [URL]

💰 TURNOVER
[₹ X Crores | FY XXXX-XX] | Source: [URL]

📍 HEAD OFFICE
[Address] | Source: [URL]

📅 YEARS IN EXISTENCE
[Founded XXXX | X years old] | Source: [URL]

👔 DIRECTORS
[Name — Designation — DIN]
[Name — Designation — DIN]
Source: [MCA URL]

🏢 BRANCHES
[X offices | Key cities] | Source: [URL]

⭐ REVIEWS & REPUTATION (Last 12 months)
Top 5 Positives:
1. ...
2. ...
Top 5 Negatives:
1. ...
2. ...
Platforms checked: [list with URLs]

🎯 OVERALL RATING: X/10
[Rationale]

🤝 KSERVE FIT ASSESSMENT
[Service] — [Fit level] — [Why]

📞 CUSTOMER CARE NUMBER
[Number] | Source: [URL]

📱 SOCIAL MEDIA FOLLOWERS
LinkedIn: X | Instagram: X | Facebook: X | Twitter: X
Source: [URLs]

📊 TRACXN
[Score / Not listed] | Source: [URL]

🔀 ACQUISITIONS & M&A
[Summary or "No recent M&A activity found"] | Source: [URL]

🧠 BD INTELLIGENCE BRIEFING
Things to know: ...
Conversation starters: ...
Trigger signals: ...
Potential objections: ...
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

---

## Core Research Principles

**Recency first:** Always prioritize sources from the last 12 months. If only older data is available, use it but clearly flag it with the date found and a note like: *"⚠️ Most recent data available — FY2022-23. Newer filings may not yet be public."*

**Every data point needs a source:** Never present a fact without a URL or document reference. If something cannot be sourced, say "Not publicly available" rather than guessing.

**Worker → Checker loop:** The Checker agent should ask: Is the data accurate? Is the source credible? Is it recent? Is it clearly attributed? Only approve when all four are yes.

**MCA is ground truth for Indian companies:** For incorporation date, directors, registered address, and financial filings — MCA (mca.gov.in) is the most authoritative source. Tofler, Zauba Corp, and similar aggregators pull from MCA and are acceptable secondary sources.

**BD framing throughout:** Every section should be written with the lens of "how does this help KServe win this account?" — not just raw data but insight.

---

## Multi-Agent Architecture (Claude Code)

When running in Claude Code with subagents enabled:

```
User confirms company (Step 1)
         │
         ▼
┌─────────────────────────────────────────┐
│         SPAWN ALL SIMULTANEOUSLY        │
│  Worker-2   Worker-3   Worker-4  ...    │
│  Worker-5   Worker-6   Worker-7  ...    │
│  Worker-8   Worker-9   Worker-10 ...    │
│  Worker-11  Worker-12  Worker-13 ...    │
│  Worker-14  Worker-15               │
└─────────────────────────────────────────┘
         │ (each worker ↔ checker loop)
         ▼
┌─────────────────────────────────────────┐
│         CHECKER AGENT (shared)          │
│  Validates: accuracy, source, recency   │
│  Returns to worker if any fail          │
└─────────────────────────────────────────┘
         │ (all approved outputs)
         ▼
┌─────────────────────────────────────────┐
│         MAIN / ORCHESTRATOR AGENT       │
│  Combines all 14 approved sections      │
│  Renders final BD Research Report       │
└─────────────────────────────────────────┘
```

On Claude.ai (no subagents): Run steps 2–15 sequentially with the same Worker → Checker logic applied inline for each step before moving to the next.

---

## Checker Agent Instructions

When acting as the Checker for any research step, evaluate the Worker's output against these criteria:

1. **Source present?** Every fact must have a URL or named document. No source = send back.
2. **Source credible?** Prefer official sources (MCA, company website, major publications) over anonymous forums or low-quality aggregators.
3. **Recency?** Is the data from the last 12 months? If older, is it flagged?
4. **Accurate?** Does the data make internal sense? (e.g., a 2-year-old company can't have 50 years of history)
5. **Complete?** Did the Worker answer everything the step requires, or are there gaps?

If any criterion fails, return to Worker with specific actionable feedback: *"The turnover figure has no source — please find the MCA filing or a news article citing the exact revenue."*

Only approve when all five criteria are met.
