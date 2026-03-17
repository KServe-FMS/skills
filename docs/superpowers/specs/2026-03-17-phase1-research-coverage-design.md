# Phase 1 Research Coverage — Design Spec

**Date:** 2026-03-17
**Scope:** `company-research/SKILL.md`
**Status:** Approved — ready for implementation

---

## Overview

Adds 5 new research modules from ROADMAP.md Phase 1 to the company-research skill:

| Module | Placement | Type |
|---|---|---|
| Employee Headcount & Growth Trend | Extend Step 7B | Extension |
| Regulatory & Legal Risk | Extend Step 14 | Extension |
| Key Partnerships & Integrations | Extend Step 14 | Extension |
| Current Outsourcing Vendors | New Step 16 | New step |
| Competitive Landscape | New Step 17 | New step |

---

## Step 7B — Extension: Employee Headcount & Growth Trend

**Rename:** "Job Postings & Workforce Signals" (was "Job Postings (Outsourcing Intent Signals)")

**New content** appended after the existing job postings BD signal line, before the Source line:

### Research
Search LinkedIn company page for current employee count and any displayed growth percentage. Cross-reference with Crunchbase employee range.

**Sources:**
1. LinkedIn company page — employee count + displayed growth % (e.g., "+18% in 2 years")
2. Crunchbase — employee range as cross-reference

**Find:**
- Current LinkedIn employee count (or band if only a range is shown)
- Displayed growth % if LinkedIn surfaces it
- Directional classification: `Growing` / `Stable` / `Shrinking` / `Insufficient data`
- Correlation with job postings: high posting volume + growing headcount = scaling pain; few/no postings + flat/declining headcount = cost-cutting mode

**BD framing:**
- Scaling → outsourcing appetite; pitch capacity and speed
- Hiring freeze / shrinking → cost-conscious; lead with cost-per-transaction vs. in-house

**Output block** (appended to Step 7B output):
```
LinkedIn Headcount: ~X employees [as of YYYY-MM-DD]
Trend: Growing / Stable / Shrinking / Insufficient data
Basis: [e.g., "+18% per LinkedIn over 2 years; corroborated by 23 open roles on Naukri"]
BD signal: [scaling pain → outsourcing appetite / freeze → cost-conscious pitch, lead with ROI]
```

**Source Priority table update:** Append to Step 7B row — LinkedIn company page (headcount) as primary; Crunchbase range as secondary.

**ICP Score:** "Employee headcount proxy" dimension already references Steps 3, 7, 7B — new LinkedIn data feeds directly into it. No scoring logic change needed.

---

## Step 14 — Extension: Regulatory & Legal Risk + Key Partnerships & Integrations

**Rename:** "M&A, Legal Risk & Key Partnerships" (was "Acquisitions & M&A Activity")

Two new sub-sections appended after the existing PE ownership / BD signal block.

---

### Sub-section: Regulatory & Legal Risk

**Sources (try in order):**
1. MCA filing status — check if annual returns / AOC-4 are overdue via Tofler or Zauba Corp
2. News search: `"[company name]" "legal notice" OR "court case" OR "SEBI" OR "RBI" OR "regulatory action"`
3. Consumer court portals: consumerforum.in, National Consumer Helpline database
4. SEBI enforcement orders: sebi.gov.in; RBI press releases: rbi.org.in

**Find:**
- MCA compliance status: filings current, overdue, or struck-off risk
- Consumer court cases filed against the company (count + nature if visible)
- SEBI or RBI enforcement notices
- Any other material litigation in public record

**BD framing rules:**
- Compliance gaps / court cases → urgency trigger + pitch KServe's documentation accuracy and audit-trail credentials
- Clean record → reliability framing ("you're compliance-conscious — so is KServe")
- SEBI/RBI action → high-distress signal; approach carefully, but outsourcing cost reduction is directly relevant

**Output block:**
```
⚖️ REGULATORY & LEGAL RISK
MCA compliance: [Clean — filings current / Overdue: X filings / Struck-off risk / Unable to verify]
Consumer court: [X cases found — [nature] / None found]
SEBI / RBI: [Notice found: [summary] / None found]
BD signal: [distress → urgency + compliance credentials / clean → reliability framing]
Source(s): [URLs] | Confidence: HIGH/MED/LOW | Checked: YYYY-MM-DD
```

---

### Sub-section: Key Partnerships & Integrations

Covers business-level strategic alliances and distribution tie-ups. Technology vendor relationships (CRM, support tools) belong in Step 7C — do not duplicate them here.

**Sources (try in order):**
1. Company website — Partners, Integrations, or Ecosystem page
2. Press releases: `"[company name]" "partnership" OR "alliance" OR "tie-up" OR "integration"`
3. LinkedIn company updates (last 12 months)
4. Tracxn / Crunchbase partnerships section

**Find:**
- Named strategic partners (distribution alliances, co-marketing, formal tie-ups)
- Business-level integrations beyond tech tools (e.g., "official partner of HDFC Bank," "distribution tie-up with BigBasket")
- Direction signal: what does the partner ecosystem reveal about where the company is heading?

**BD framing:** A company actively building a partner network is culturally open to new vendor relationships. Named partners can serve as warm referral angles if KServe already works with them.

**Output block:**
```
🤝 KEY PARTNERSHIPS & INTEGRATIONS
[Partner name — nature of alliance — BD implication]
[Repeat for each named partner, or "No public partnerships found"]
BD signal: [partner ecosystem direction / referral angle if KServe knows the partner]
Source(s): [URLs] | Confidence: HIGH/MED/LOW | Source date: YYYY-MM-DD
```

**Source Priority table update:** Append to Step 14 row — consumerforum.in, sebi.gov.in, rbi.org.in for regulatory sub-section; company website Partners page, LinkedIn updates for partnerships sub-section.

---

## New Step 16 — Current Outsourcing Vendors

**Placement:** After Step 15 in the step sequence. Runs in Wave 1 (fully independent, no dependencies).

Knowing which BPO vendors are already embedded changes the pitch angle from "you need this" to "here's why KServe is better."

**Sources (try in order):**
1. News: `"[company name]" "outsourcing" OR "BPO" OR "outsourced to" OR "BPO partner"` — ET, Mint, Business Standard
2. Job postings from Step 7B: scan JD language for "coordinate with outsourcing vendor," "manage BPO partner," "work with third-party vendor"
3. LinkedIn company updates / press releases on company website
4. General search: `"[company name]" "call center partner" OR "back office partner" OR "collections agency"`

**Find:**
- Named outsourcing/BPO vendors already in use
- Functions being outsourced (CS, collections, back-office, lead gen, etc.)
- Any indication of contract vintage (fresh engagement vs. long-standing)
- If no vendor found: explicitly state "No outsourcing vendor relationships found in public record"

**BD framing rules:**
- No vendor found → greenfield; pitch as first mover, zero displacement risk
- Competitor BPO vendor found → displacement pitch; lead with KServe's AI differentiation and cost-per-transaction comparison
- Non-BPO vendor found (in-house only, freelance) → expansion pitch; they've started outsourcing, KServe can professionalize it
- KServe-adjacent industry client found → name-drop the relevant case study in outreach

**Checker note:** If no results found after all 4 source attempts, Worker must explicitly state "No results found" — not infer absence from general company maturity signals.

**Output block:**
```
🏭 CURRENT OUTSOURCING VENDORS
Vendors detected:
  [Vendor name] — [function outsourced] — [source]
  [Or: "No outsourcing vendor relationships found in public record"]
BD signal: [greenfield / displacement / expansion angle — specific pitch implication]
Source(s): [URLs] | Confidence: HIGH/MED/LOW | Checked: YYYY-MM-DD
```

**Source Priority table row:**

| Step | Primary | Secondary | Fallback |
|---|---|---|---|
| 16 — Outsourcing Vendors | News (ET · Mint · BS): `"[company]" "BPO" OR "outsourcing"` | Step 7B JD language scan | LinkedIn updates · company website press releases |

---

## New Step 17 — Competitive Landscape

**Placement:** After Step 16 in the step sequence. Runs in Wave 1 (fully independent, no dependencies).

**Sources (try in order):**
1. Tracxn — "Similar companies" section on the company's Tracxn profile
2. Crunchbase — "Similar companies" or "Competitors" tab
3. Search: `"[company name] competitors" OR "top [industry] companies India [year]"`
4. Industry directories or rankings (e.g., Inc42, YourStory for startups; CRISIL/ICRA sector reports for traditional companies)

**Find:**
- Top 3 direct competitors by name
- One-line descriptor for each (size signal, market position, or funding stage if known)
- Whether KServe already serves any of these competitors — if yes, flag as case study reference
- Whether any competitor is visibly outpacing the prospect (signals urgency)

**BD framing rules:**
- KServe already serves a competitor → name it in outreach as social proof in the same vertical
- A competitor is larger/better-funded → urgency hook: "they're scaling faster — outsourcing operations lets you keep pace without the headcount cost"
- No competitive data found → write "No public competitor data found" — do not guess from general industry knowledge

**Output block:**
```
🏆 COMPETITIVE LANDSCAPE
1. [Competitor name] — [descriptor: size / funding / market position]
2. [Competitor name] — [descriptor]
3. [Competitor name] — [descriptor]
[Or: "No public competitor data found on Tracxn, Crunchbase, or search"]
BD signal: [case study tie-in / competitive urgency angle]
Source(s): [URLs] | Confidence: HIGH/MED/LOW | Checked: YYYY-MM-DD
```

**Source Priority table row:**

| Step | Primary | Secondary | Fallback |
|---|---|---|---|
| 17 — Competitive Landscape | Tracxn "Similar companies" | Crunchbase "Competitors" tab | News/industry rankings: `"[company] competitors"` |

---

## Integration Changes

### PARALLEL wave structure

**Wave 1** — update spawn list from 15 to 17 workers:
- Add Steps 16 and 17 to Wave 1 (both fully independent)
- Updated list: `2, 3, 4, 5, 6, 6B, 7, 7B, 7C, 8, 9, 11, 12, 13, 14, 16, 17`

**Wave 2** — unchanged: Steps 10 and 10B only.

**Progress status board** — update after Wave 1 spawn:
- "Running 17 parallel workers" (was 15)
- In-progress line: `⏳ In progress: Steps 2, 3, 4, 5, 6, 6B, 7, 7B, 7C, 8, 9, 11, 12, 13, 14, 16, 17`

**Orchestrator worker count** — update "After all 17 Workers complete" → "After all 19 Workers complete"

### Step 14 rename — two locations
1. Step header: `### Step 14 — M&A, Legal Risk & Key Partnerships`
2. Output format section header: `🔀 M&A, LEGAL RISK & KEY PARTNERSHIPS`

### Output format template — three insertion points

1. **Step 7B block** — append headcount block after existing BD signal line, before Source line
2. **Step 14 block** — append `⚖️ REGULATORY & LEGAL RISK` and `🤝 KEY PARTNERSHIPS & INTEGRATIONS` blocks after existing PE ownership / BD signal block
3. **After Step 15 block** — add in order:
   - `🏭 CURRENT OUTSOURCING VENDORS`
   - `🏆 COMPETITIVE LANDSCAPE`

### No changes required
- Checker criteria (all 7 apply as-is to new steps)
- ICP Score dimensions and scoring logic
- Step 10 / 10B dependency logic
- Wave 2 spawn rules
- SEQUENTIAL mode step order (Steps 16 and 17 run after Step 15 naturally)
