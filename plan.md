# Plan: Phase 1 — Depth Improvements to Existing Steps (Pending Items)

**Date:** 2026-04-04
**File:** `company-research/SKILL.md`
**Scope:** Four pending `[ ]` items from ROADMAP.md § Phase 1 → Depth Improvements to Existing Steps

---

## Approach

All four items are targeted extensions to existing step instructions and their corresponding output format blocks. No new steps, no wave changes, no orchestrator count changes. Each item:
1. Extends the step instruction with new sub-section content
2. Updates the Output Format block for that step
3. Updates the Source Priority Reference table row where needed

One plan.md commit per item for clean git history.

---

## Specifics

### Item 1 — Step 3: Turnover Trend (3-Year)

**Instruction change:** Replace the single-sentence "Find annual revenue/turnover" paragraph with a version that requires the latest year's figure as mandatory and then attempts the prior 2 years for trend context. Years are dynamic — always relative to the current date, never hardcoded.

**New instruction content:**
```
Find annual revenue/turnover in Indian Rupees (Crores). The **most recent financial year** is mandatory — always report it. Then attempt to retrieve the **2 prior financial years** (i.e., the last 3 financial years total) for trend context.

For Indian-registered companies: use MCA annual filings → Tofler/Zauba → news.
For non-Indian companies or Indian subsidiaries of foreign entities: report in original currency, convert to INR at filing-date exchange rate, and note in report: `Revenue in [currency]; converted to INR at [rate] as of [date].`
If a prior year is not publicly available: write `[FY label]: Not available` for that year.
If the latest year is unavailable: write "Private company — turnover not publicly disclosed." and omit the trend section.

**Trend classification (requires at least 2 years of data):**
- `Growing` — each available year higher than prior
- `Declining` — each available year lower than prior
- `Mixed` — revenue fluctuated across years
- `Insufficient data` — only 1 year available; trend cannot be determined

**BD framing:**
- Growing trend → company is expanding; pitch capacity and speed ("we scale with you")
- Declining trend → cost pressure is real; lead with cost-per-transaction vs. in-house
- Mixed trend → probe for context (acquisition year, market disruption); don't lead with growth assumptions
```

**Source Priority table:** No change needed — existing sources (Tofler, Zauba, MCA, news) cover multi-year data.

**Output format change:** Replace the current single-line `💰 TURNOVER` block with a dynamic 3-year layout and trend line:

```
💰 TURNOVER
[Most recent FY]: ₹[X] Cr | [Prior FY]: ₹[X] Cr | [FY before that]: ₹[X] Cr (or "Not available")
Trend: Growing / Declining / Mixed / Insufficient data
BD signal: [growth → scale pitch / decline → cost-reduction pitch / mixed → probe before assuming]
Source(s): [URL] | Confidence: HIGH/MED/LOW | Source date: YYYY-MM-DD
```

---

### Item 2 — Step 6: Board Composition Signal

**Instruction change:** Append a "Board Composition Signal" sub-section after the existing LinkedIn lookup block (before the output format template section). Classification is derived from MCA designations only — no additional research required.

**New instruction content:**
```
**Board Composition Signal:**
Using the director list from MCA, classify the board as one of:
- `Founder-dominated` — MD/CEO/Promoter-Director(s) hold the majority of board seats AND are also promoters/shareholders
- `Institutional` — majority of seats held by Independent Directors or PE/VC-nominated directors; founder(s) hold minority or no seats
- `Mixed` — roughly equal split between founder and independent/institutional directors, or both founder and PE/institutional voice are clearly present

**Classification rules:**
- Designation signals: "Managing Director", "Promoter Director", "Director (Promoter)" → founder side
- Designation signals: "Independent Director", "Nominee Director", "Non-Executive Director" → institutional side
- If designation data is ambiguous or unavailable from MCA: write `Board classification: Insufficient data — designations not available`

**BD framing:**
- Founder-dominated → single decision-maker or small inner circle; deal can close faster; pitch to the MD directly
- Institutional → multi-stakeholder buy-in required; expect a longer evaluation cycle; include ROI data and case studies in first contact
- Mixed → adapt per the strongest voice found in Step 6B dossiers
```

**Source Priority table:** No change — Step 6 row already includes MCA as primary source.

**Output format change:** Add a Board Classification line after the director list in `👔 DIRECTORS`:

```
👔 DIRECTORS
★ [Name] — [Designation] — DIN: [XXXXXXXX] — LinkedIn: [URL or "Not accessible"] — Tenure: [X years / ★ NEW (<6 months)]
[Name] — [Designation] — DIN: [XXXXXXXX]
Board Classification: Founder-dominated / Institutional / Mixed / Insufficient data
BD signal: [decision-making speed implication and recommended pitch approach]
Source(s): [MCA URL] | Confidence: HIGH/MED/LOW | Source date: YYYY-MM-DD
```

---

### Item 3 — Step 7B: Attrition Signal from JDs

**Instruction change:** Extend the existing "Keywords in JDs" bullet with an attrition-specific keyword set, and add an "Attrition Signal" as a distinct Find bullet + BD framing rule.

**Keyword addition:** After the existing outsourcing-pain keyword list, add:
```
- Attrition signals in JDs — flag separately from outsourcing pain: "replacement hire," "immediate joiners," "notice period buyout," "backfill," "high-volume hiring," "we are continuously hiring" (for the same role type)
```

**Find addition:** Add a bullet after the KServe-relevant roles bullet:
```
- Attrition signal: are any open roles in functions KServe serves phrased as replacement hires or immediate-joiner urgency? If yes, flag the function and the keyword found.
```

**BD framing addition:** Add a rule after the existing BD framing block:
```
- High attrition in a KServe-relevant function (flagged by replacement / immediate-joiner language) → strongest outsourcing trigger: the company is losing productivity every hiring cycle; outsourcing removes the attrition cost entirely. Lead with: "We've helped companies in [industry] eliminate recurring backfill cost in [function] by transitioning to a managed-ops model."
```

**Output format change:** Add an Attrition Signal line after the Headcount signal line in `💼 JOB POSTINGS & WORKFORCE SIGNALS`:

```
Attrition signal: [High — [function] JDs show replacement/immediate-joiner language / None detected / Insufficient data]
```

---

## Scope

- **Files modified:** `company-research/SKILL.md` only
- **ROADMAP.md:** 3 items marked `[x]` as a final commit
- **No wave, orchestrator, or step count changes**
- **No new steps, no new Source Priority table rows**

---

## Artifacts

| File | Change |
|------|--------|
| `company-research/SKILL.md` | 3 instruction extensions + 3 output format additions |
| `ROADMAP.md` | 3 items marked shipped |

---

## Considerations

- Step 3: latest year is mandatory; prior 2 years are best-effort for trend. Single-year fallback (`Insufficient data`) is explicitly handled. Years are always relative to current date — never hardcoded.
- Board Composition Signal uses MCA designations only — no additional search steps, no dependency on LinkedIn, no wave changes.
- Attrition signal keywords are labeled as a distinct category in the instruction to prevent conflation with the outsourcing-pain keyword set.

---

## Impact

- **BD value:** Each item converts raw data (single-year turnover, raw director list, unclassified JD keywords) into an actionable signal with an explicit pitch-angle implication.
- **No regressions:** All changes are additive. Existing Worker output fields remain unchanged; new fields are appended.
- **Checker coverage:** No Checker criterion changes needed — new content falls within existing BD Relevance scope for Steps 3, 6, and 7B.

---

## Task List

- [ ] **Task 1A:** Extend Step 3 instruction — mandatory latest year + 2 prior years for trend + trend classification + BD framing
- [ ] **Task 1B:** Update Step 3 output format block (`💰 TURNOVER`)
- [ ] **Task 1C:** Verify Step 3 changes and commit
- [ ] **Task 2A:** Add Board Composition Signal sub-section to Step 6 instruction
- [ ] **Task 2B:** Update Step 6 output format block (`👔 DIRECTORS`)
- [ ] **Task 2C:** Verify Step 6 changes and commit
- [ ] **Task 3A:** Extend Step 7B instruction — attrition keywords + Find bullet + BD framing rule
- [ ] **Task 3B:** Update Step 7B output format block (`💼 JOB POSTINGS & WORKFORCE SIGNALS`)
- [ ] **Task 3C:** Verify Step 7B changes and commit
- [ ] **Task 4:** Mark 3 ROADMAP.md items `[x]` and commit
