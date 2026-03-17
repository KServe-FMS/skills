# Phase 1 Research Coverage Implementation Plan

> **For agentic workers:** REQUIRED: Use superpowers:subagent-driven-development (if subagents available) or superpowers:executing-plans to implement this plan. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Add 5 new research modules to `company-research/SKILL.md` — Employee Headcount, Regulatory & Legal Risk, Key Partnerships, Current Outsourcing Vendors, and Competitive Landscape.

**Architecture:** All changes are targeted edits to a single Markdown file (`company-research/SKILL.md`). Each task modifies a specific named section of the file using exact find-and-replace. No build or test tooling exists — verification is done by grepping for the new text after each edit.

**Tech Stack:** Markdown/YAML only. Edit tool for targeted changes, Grep tool for verification.

---

## Chunk 1: Step 7B — Rename and Add Headcount Content

### Task 1: Rename Step 7B headers and update Source Priority row

**Files:**
- Modify: `company-research/SKILL.md`

- [ ] **Step 1: Rename the Step 7B instruction section header**

Find and replace:
```
old: ### Step 7B — Job Postings (Outsourcing Intent Signals)
new: ### Step 7B — Job Postings & Workforce Signals
```

- [ ] **Step 2: Verify step header rename**

Run: `grep -n "^### Step 7B" company-research/SKILL.md`
Expected: one line reading `### Step 7B — Job Postings & Workforce Signals`

- [ ] **Step 3: Update the Source Priority table row for Step 7B**

Find and replace (exact row):
```
old: | 7B — Job Postings | Naukri (site:naukri.com "[company]") | LinkedIn Jobs · Indeed India | Company careers page |
new: | 7B — Job Postings & Workforce Signals | Naukri (site:naukri.com "[company]") · LinkedIn company page (headcount) | LinkedIn Jobs · Indeed India · Crunchbase (employee range) | Company careers page |
```

- [ ] **Step 4: Verify Source Priority row update**

Run: `grep -n "7B.*LinkedIn company page (headcount)" company-research/SKILL.md`
Expected: exactly one match in the Source Priority table

- [ ] **Step 5: Add Employee Headcount research content to Step 7B instructions**

Find and replace in the Step 7B section. Insert new content after the "If no public job postings found" paragraph and before the Source line:

```
old:
**If no public job postings found:** Write `No active job postings found on Naukri, LinkedIn Jobs, or Indeed India as of [date]. Company may not be publicly recruiting, or postings may be behind a login wall.`

Source(s): [URLs] | Confidence: HIGH/MED/LOW | Checked: YYYY-MM-DD

new:
**If no public job postings found:** Write `No active job postings found on Naukri, LinkedIn Jobs, or Indeed India as of [date]. Company may not be publicly recruiting, or postings may be behind a login wall.`

**Employee Headcount & Growth Trend:**
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

Source(s): [URLs] | Confidence: HIGH/MED/LOW | Checked: YYYY-MM-DD
```

- [ ] **Step 6: Verify headcount content added**

Run: `grep -n "Employee Headcount" company-research/SKILL.md`
Expected: one match in the Step 7B section

- [ ] **Step 7: Rename the Step 7B output format template header**

Find and replace inside the Output Format code block:
```
old: 💼 JOB POSTINGS (Intent Signals)
new: 💼 JOB POSTINGS & WORKFORCE SIGNALS
```

- [ ] **Step 8: Add headcount output block to the Step 7B output template**

Find and replace in the Output Format section:
```
old:
BD signal: [what this hiring pattern implies about resourcing pressure]
Source(s): [URLs] | Confidence: HIGH/MED/LOW | Checked: YYYY-MM-DD

🛠️ TECHNOLOGY STACK

new:
BD signal: [what this hiring pattern implies about resourcing pressure]
LinkedIn Headcount: ~X employees [as of YYYY-MM-DD]
Trend: Growing / Stable / Shrinking / Insufficient data
Basis: [e.g., "+18% per LinkedIn over 2 years; corroborated by 23 open roles on Naukri"]
Headcount signal: [scaling pain → outsourcing appetite / freeze → cost-conscious pitch, lead with ROI]
Source(s): [URLs] | Confidence: HIGH/MED/LOW | Checked: YYYY-MM-DD

🛠️ TECHNOLOGY STACK
```

Note: The job postings `BD signal:` label is preserved from the existing output block. The headcount signal uses `Headcount signal:` to distinguish the two dimensions.

- [ ] **Step 9: Verify output template updates**

Run: `grep -c "WORKFORCE SIGNALS\|LinkedIn Headcount\|Headcount signal" company-research/SKILL.md`
Expected: 3 (header rename + LinkedIn Headcount field + Headcount signal label)

- [ ] **Step 10: Commit**

```bash
git add company-research/SKILL.md
git commit -m "feat: Step 7B — add Employee Headcount & Growth Trend"
```

---

## Chunk 2: Step 14 — Rename and Add Regulatory + Partnerships Sub-sections

### Task 2: Rename Step 14 and add Regulatory & Legal Risk sub-section

**Files:**
- Modify: `company-research/SKILL.md`

- [ ] **Step 1: Rename the Step 14 instruction section header**

Find and replace:
```
old: ### Step 14 — Acquisitions & M&A Activity
new: ### Step 14 — M&A, Funding, Legal Risk & Key Partnerships
```

- [ ] **Step 2: Verify step header rename**

Run: `grep -n "^### Step 14" company-research/SKILL.md`
Expected: one line reading `### Step 14 — M&A, Funding, Legal Risk & Key Partnerships`

- [ ] **Step 3: Update the Source Priority table row for Step 14**

Find and replace (exact row):
```
old: | 14 — M&A | News (last 12 months) | Tracxn · Crunchbase · MCA filings · gem.gov.in | ET · Mint · Business Standard |
new: | 14 — M&A, Funding, Legal Risk & Key Partnerships | News (last 12 months) · consumerforum.in · sebi.gov.in · rbi.org.in · Company website Partners page · LinkedIn company updates | Tracxn · Crunchbase · MCA filings · gem.gov.in · Tofler / Zauba Corp (MCA compliance) | ET · Mint · Business Standard |
```

- [ ] **Step 4: Verify Source Priority row update**

Run: `grep -n "14 —" company-research/SKILL.md`
Expected: one line containing `M&A, Funding, Legal Risk & Key Partnerships` and `consumerforum.in`

- [ ] **Step 5: Add Regulatory & Legal Risk and Key Partnerships sub-sections to Step 14 instructions**

Find and replace. The existing BD signals block ends with `Late-stage PE backing` — append both sub-sections before the closing `---`:

```
old:
BD signals:
- Being acquired → may freeze vendor decisions (note in report)
- Fresh funding raised → likely expanding, open to outsourcing (highlight as trigger signal for Step 15)
- GeM supplier → compliance-driven, longer sales cycle, pitch with documentation accuracy and audit trails
- Late-stage PE backing → cost reduction is a stated goal; lead with cost-per-transaction vs. in-house comparison

---

### Step 15 — BD Intelligence Briefing

new:
BD signals:
- Being acquired → may freeze vendor decisions (note in report)
- Fresh funding raised → likely expanding, open to outsourcing (highlight as trigger signal for Step 15)
- GeM supplier → compliance-driven, longer sales cycle, pitch with documentation accuracy and audit trails
- Late-stage PE backing → cost reduction is a stated goal; lead with cost-per-transaction vs. in-house comparison

**Regulatory & Legal Risk:**

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

**Key Partnerships & Integrations:**
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

---

### Step 15 — BD Intelligence Briefing
```

- [ ] **Step 6: Verify sub-sections added**

Run: `grep -n "Regulatory & Legal Risk\|Key Partnerships & Integrations" company-research/SKILL.md`
Expected: two matches in the Step 14 section

- [ ] **Step 7: Rename Step 14 output format template header**

Find and replace inside the Output Format code block:
```
old: 🔀 M&A, FUNDING & OWNERSHIP
new: 🔀 M&A, FUNDING, LEGAL RISK & KEY PARTNERSHIPS
```

- [ ] **Step 8: Add Regulatory and Partnerships output blocks to Step 14 output template**

Find and replace in the Output Format section:
```
old:
BD signal: [ownership/funding implication]
Source(s): [URL] | Confidence: HIGH/MED/LOW | Source date: YYYY-MM-DD

🧠 BD INTELLIGENCE BRIEFING

new:
BD signal: [ownership/funding implication]
Source(s): [URL] | Confidence: HIGH/MED/LOW | Source date: YYYY-MM-DD

⚖️ REGULATORY & LEGAL RISK
MCA compliance: [Clean — filings current / Overdue: X filings / Struck-off risk / Unable to verify]
Consumer court: [X cases found — [nature] / None found]
SEBI / RBI: [Notice found: [summary] / None found]
BD signal: [distress → urgency + compliance credentials / clean → reliability framing]
Source(s): [URLs] | Confidence: HIGH/MED/LOW | Checked: YYYY-MM-DD

🤝 KEY PARTNERSHIPS & INTEGRATIONS
[Partner name — nature of alliance — BD implication]
[Repeat for each named partner, or "No public partnerships found"]
BD signal: [partner ecosystem direction / referral angle if KServe knows the partner]
Source(s): [URLs] | Confidence: HIGH/MED/LOW | Source date: YYYY-MM-DD

🧠 BD INTELLIGENCE BRIEFING
```

- [ ] **Step 9: Verify output template additions**

Run: `grep -n "REGULATORY & LEGAL RISK\|KEY PARTNERSHIPS & INTEGRATIONS\|LEGAL RISK & KEY PARTNERSHIPS" company-research/SKILL.md`
Expected: three matches — the header rename and both new output blocks

- [ ] **Step 10: Commit**

```bash
git add company-research/SKILL.md
git commit -m "feat: Step 14 — add Regulatory & Legal Risk and Key Partnerships sub-sections"
```

---

## Chunk 3: New Steps 16 and 17

### Task 3: Add Step 16 — Current Outsourcing Vendors

**Files:**
- Modify: `company-research/SKILL.md`

- [ ] **Step 1: Add Step 16 instruction section after Step 15**

Find and replace. Step 15 ends with `---` followed immediately by `## Output Format`. Insert Step 16 between them:

```
old:
- If ICP Score (Step 10B) is Tier 3 or Deprioritize: action = `Add to [60-day / 90-day] nurture sequence — do not assign AE yet. Monitor for: [specific trigger to watch, e.g., next funding round announcement, next Glassdoor spike]`

---

## Output Format

new:
- If ICP Score (Step 10B) is Tier 3 or Deprioritize: action = `Add to [60-day / 90-day] nurture sequence — do not assign AE yet. Monitor for: [specific trigger to watch, e.g., next funding round announcement, next Glassdoor spike]`

---

### Step 16 — Current Outsourcing Vendors

Knowing which BPO vendors are already embedded changes the pitch angle from "you need this" to "here's why KServe is better."

**Sources (try in order):**
1. News: `"[company name]" "outsourcing" OR "BPO" OR "vendor" OR "BPO partner"` — ET, Mint, Business Standard
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

**Worker note:** If no results found after all 4 source attempts, explicitly state "No outsourcing vendor relationships found in public record" — do not infer absence from general company maturity signals.

Source(s): [URLs] | Confidence: HIGH/MED/LOW | Checked: YYYY-MM-DD

---

### Step 17 — Competitive Landscape

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

**Worker note:** If no results found after all 4 source attempts, explicitly state "No public competitor data found" — do not infer from general industry knowledge.

Source(s): [URLs] | Confidence: HIGH/MED/LOW | Checked: YYYY-MM-DD

---

## Output Format
```

- [ ] **Step 2: Verify Steps 16 and 17 added**

Run: `grep -n "Step 16\|Step 17" company-research/SKILL.md`
Expected: at least two matches — one for each step header in the Research Steps section

- [ ] **Step 3: Add Source Priority table rows for Steps 16 and 17**

Find and replace. Add after the Step 15 row in the Source Priority table:

```
old:
| 15 — BD Briefing | Synthesized from Steps 2–14 output — no new searches | — | If ≥ 4 steps exhausted retries, open with partial-data warning. If Step 10 is RETRY_EXHAUSTED, omit Trigger Signals. If Step 8 RETRY_EXHAUSTED, skip review-based Conversation Starters. |

new:
| 15 — BD Briefing | Synthesized from Steps 2–14 output — no new searches | — | If ≥ 4 steps exhausted retries, open with partial-data warning. If Step 10 is RETRY_EXHAUSTED, omit Trigger Signals. If Step 8 RETRY_EXHAUSTED, skip review-based Conversation Starters. |
| 16 — Outsourcing Vendors | News (ET · Mint · BS): `"[company]" "outsourcing" OR "BPO" OR "vendor"` | Step 7B JD language scan | LinkedIn updates · company website press releases |
| 17 — Competitive Landscape | Tracxn "Similar companies" | Crunchbase "Competitors" tab | News/industry rankings: `"[company] competitors"` |
```

- [ ] **Step 4: Verify Source Priority rows added**

Run: `grep -n "16 —\|17 —" company-research/SKILL.md`
Expected: matches for both Step 16 and Step 17 rows in the Source Priority table

- [ ] **Step 5: Add Steps 16 and 17 output blocks to the Output Format template**

Find and replace. Insert the two new blocks between the Next Best Action line and the DATA QUALITY separator:

```
old:
Next Best Action:
[Do X] — [because Y] — [contact: Named Director] — [via: LinkedIn InMail / phone / email] — [hook: specific research finding]

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
📝 DATA QUALITY

new:
Next Best Action:
[Do X] — [because Y] — [contact: Named Director] — [via: LinkedIn InMail / phone / email] — [hook: specific research finding]

🏭 CURRENT OUTSOURCING VENDORS
Vendors detected:
  [Vendor name] — [function outsourced] — [source]
  [Or: "No outsourcing vendor relationships found in public record"]
BD signal: [greenfield / displacement / expansion angle — specific pitch implication]
Source(s): [URLs] | Confidence: HIGH/MED/LOW | Checked: YYYY-MM-DD

🏆 COMPETITIVE LANDSCAPE
1. [Competitor name] — [descriptor: size / funding / market position]
2. [Competitor name] — [descriptor]
3. [Competitor name] — [descriptor]
[Or: "No public competitor data found on Tracxn, Crunchbase, or search"]
BD signal: [case study tie-in / competitive urgency angle]
Source(s): [URLs] | Confidence: HIGH/MED/LOW | Checked: YYYY-MM-DD

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
📝 DATA QUALITY
```

- [ ] **Step 6: Verify output blocks added**

Run: `grep -n "CURRENT OUTSOURCING VENDORS\|COMPETITIVE LANDSCAPE" company-research/SKILL.md`
Expected: two matches in the Output Format section

- [ ] **Step 7: Commit**

```bash
git add company-research/SKILL.md
git commit -m "feat: add Steps 16 (Outsourcing Vendors) and 17 (Competitive Landscape)"
```

---

## Chunk 4: Integration Changes

### Task 4: Update wave structure, counts, and architecture references

**Files:**
- Modify: `company-research/SKILL.md`

- [ ] **Step 1: Update Wave 1 spawn list**

Find and replace:
```
old: **Wave 1 — spawn simultaneously:** Workers 2, 3, 4, 5, 6, 6B, 7, 7B, 7C, 8, 9, 11, 12, 13, 14. Each Worker runs its own Checker loop independently.
new: **Wave 1 — spawn simultaneously:** Workers 2, 3, 4, 5, 6, 6B, 7, 7B, 7C, 8, 9, 11, 12, 13, 14, 16, 17. Each Worker runs its own Checker loop independently.
```

- [ ] **Step 2: Update progress status board — worker count and in-progress list**

Find and replace:
```
old:
Research started for [Company Name]. Running 15 parallel workers:
⏳ In progress: Steps 2, 3, 4, 5, 6, 6B, 7, 7B, 7C, 8, 9, 11, 12, 13, 14

new:
Research started for [Company Name]. Running 17 parallel workers:
⏳ In progress: Steps 2, 3, 4, 5, 6, 6B, 7, 7B, 7C, 8, 9, 11, 12, 13, 14, 16, 17
```

- [ ] **Step 3: Verify wave structure changes**

Run: `grep -n "parallel workers\|spawn simultaneously" company-research/SKILL.md`
Expected: "Running 17 parallel workers" and "Workers 2, 3, 4, 5, 6, 6B, 7, 7B, 7C, 8, 9, 11, 12, 13, 14, 16, 17"

- [ ] **Step 4: Update PARALLEL architecture ASCII diagram**

Find and replace:
```
old: │           8, 9*, 11, 12, 13, 14                     │
new: │           8, 9*, 11, 12, 13, 14, 16, 17             │
```

- [ ] **Step 5: Verify diagram update**

Run: `grep -n "9\*, 11, 12, 13, 14" company-research/SKILL.md`
Expected: one match containing `, 16, 17`

- [ ] **Step 6: Update SEQUENTIAL mode step count**

Find and replace:
```
old: Run all 14 research steps (Steps 2–15) using the execution mode detected above.
new: Run all 16 research steps (Steps 2–17) using the execution mode detected above.
```

- [ ] **Step 7: Update Orchestrator worker count**

Find and replace:
```
old: After all 17 Workers complete and each Checker has approved:
new: After all 19 Workers complete and each Checker has approved:
```

- [ ] **Step 8: Update DATA QUALITY footer example in output template**

Find and replace:
```
old: Overall: [e.g., 9/14 fields HIGH · 3 MED · 2 LOW]
new: Overall: [e.g., 9/16 fields HIGH · 5 MED · 2 LOW]
```

- [ ] **Step 9: Update Orchestrator tally instruction (prose and inline example)**

Find and replace:
```
old: 6. Tally confidence levels across all 14 sections and populate the "Overall" line in the DATA QUALITY footer (e.g., `9/14 HIGH · 3 MED · 2 LOW`). Find the oldest source date across all sections and populate "Oldest source".
new: 6. Tally confidence levels across all 16 sections and populate the "Overall" line in the DATA QUALITY footer (e.g., `9/16 HIGH · 5 MED · 2 LOW`). Find the oldest source date across all sections and populate "Oldest source".
```

- [ ] **Step 10: Update SEQUENTIAL mode diagram to show Steps 16 and 17**

The SEQUENTIAL architecture diagram ends with `│ Step 15  │` as the last step. Extend it to include Steps 16 and 17:

Find and replace:
```
old:
    ┌────▼─────┐
    │ Step 15  │ Worker → Checker validates → approved ✓
    └────┬─────┘
         │
         ▼
  Orchestrator assembles and presents final report

new:
    ┌────▼─────┐
    │ Step 15  │ Worker → Checker validates → approved ✓
    └────┬─────┘
    ┌────▼─────┐
    │ Step 16  │ Worker → Checker validates → approved ✓
    └────┬─────┘
    ┌────▼─────┐
    │ Step 17  │ Worker → Checker validates → approved ✓
    └────┬─────┘
         │
         ▼
  Orchestrator assembles and presents final report
```

- [ ] **Step 11: Verify SEQUENTIAL diagram update**

Run: `grep -n "Step 16\|Step 17" company-research/SKILL.md`
Expected: matches in both the Research Steps section (instruction headers) and the SEQUENTIAL diagram

- [ ] **Step 12: Verify all integration changes**

Run: `grep -n "16 research steps\|19 Workers\|9/16\|all 16 sections\|16, 17" company-research/SKILL.md`
Expected: at least 5 distinct matches covering each change

- [ ] **Step 13: Commit**

```bash
git add company-research/SKILL.md
git commit -m "feat: update wave structure, orchestrator counts, and sequential diagram for Steps 16 & 17"
```

---

## Final Verification

- [ ] **Confirm ROADMAP.md items can be marked done**

The following Phase 1 items are now implemented. Mark them `[x]` in `ROADMAP.md`:

```
- [x] **Employee Headcount & Growth Trend** — LinkedIn `#employees` over time; signals scaling pain or hiring freeze
- [x] **Current Outsourcing Vendors** — detect competitors already embedded via news/announcements; changes the pitch angle entirely
- [x] **Regulatory & Legal Risk** — MCA compliance defaults, consumer court cases, SEBI/RBI notices; distress is both risk and opportunity
- [x] **Competitive Landscape** — top 3 competitors; positions KServe to cite relevant case studies
- [x] **Key Partnerships & Integrations** — strategic alliances signal direction and potential entry points
```

- [ ] **Final commit**

```bash
git add ROADMAP.md
git commit -m "docs: mark Phase 1 research coverage items complete in ROADMAP"
```
