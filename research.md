# Research: Phase 1 — Depth Improvements to Existing Steps (Pending Items)

**Date:** 2026-04-04
**Scope:** Four pending items from ROADMAP.md § Phase 1 → Depth Improvements to Existing Steps

---

## What Exists Today

### Item 1: Step 3 — Turnover Trend (3-Year)

**Current state (SKILL.md line 247):**
```
Find annual revenue/turnover in Indian Rupees (Crores). Always include the financial year (e.g., FY2023-24).
For Indian-registered companies: use MCA annual filings → Tofler/Zauba → news.
...
If not publicly available: write "Private company — turnover not publicly disclosed."
```
Step 3 collects a single year's turnover. No multi-year trend logic, no directional classification, no pitch-angle pivot based on trend direction.

**Output format block (line ~1040–1060 in SKILL.md — Output Format section):**
The output for Step 3 is a simple `💰 TURNOVER` block with one figure and one source line. No trend table.

**Source Priority table row for Step 3:**
`| 3 — Turnover | Tofler (tofler.in) · Zauba Corp (zaubacorp.com) | MCA directly (mca.gov.in) | ET · Mint · Business Standard |`

---

### Item 2: Step 6 — Board Composition Signal

**Current state (lines 271–290):**
Step 6 pulls directors from MCA with names, designations, and DINs. BD-relevant directors (MD, COO, CFO, VP Operations) are ★-flagged for LinkedIn lookup. Step 6B (Decision-Maker Dossiers, Wave 2) builds dossiers on ★-flagged directors.

No classification of board type. The board structure is implicit in the designation list but never synthesized into a decision-making speed signal.

**Gap:** Knowing whether a board is Founder-dominated, Institutional, or Mixed changes which pitch approach to use and how many stakeholders to expect in a buying decision. Currently that inference is left entirely to the BD rep.

**Step 6B dependency:** Board Composition Signal is an aggregate classification — it can be derived from the director list produced by Step 6. It does not require LinkedIn data (which is Wave 2 territory). It should live in Step 6 itself, not Step 6B.

**Output format block for Step 6:** Currently lists directors in a table, ★-flagged. No classification line.

**Source Priority table row for Step 6:** `| 6 — Directors | MCA (mca.gov.in) · Tofler DIN lookup | Zauba Corp | LinkedIn (for ★-flagged names only) |`

---

### Item 3: Step 7B — Attrition Signal from JDs

**Current state (lines 317–357):**
Step 7B already scans JD language for outsourcing pain signals:
```
Keywords in JDs that signal outsourcing pain: "manage high volume," "handle escalations," "coordinate with outsourcing vendor," "work with BPO partner," "process-driven," "high-throughput"
```
The "Find" block captures KServe-relevant role types. The BD framing paragraph provides a 1-sentence signal.

**Gap:** Attrition-signal keywords ("replacement hire," "immediate joiners," "notice period buyout") are not in the keyword list and not in the Find or BD framing sections. These keywords indicate that the company is back-filling departed staff rather than growing — a different and stronger outsourcing trigger: if attrition is high in a function KServe serves, the company is losing productivity every hiring cycle and is a natural candidate to hand off that function entirely.

**Integration point:** The attrition signal belongs in the existing JD keyword scan — it's the same Worker action, just an extended keyword list plus an additional classification output line.

---

### Item 4: GeM Supplier Profile Depth (Step 14)

**Current state (lines 693–694):**
```
- **Government contracts:** Search `gem.gov.in "[company name]"` — note if they are an active GeM (Government e-Marketplace) supplier. This signals compliance maturity, longer procurement timelines, and that the company operates in regulated environments. BD implication: open with compliance and documentation-quality credentials.
```
And in BD signals:
```
- GeM supplier → compliance-driven, longer sales cycle, pitch with documentation accuracy and audit trails
```

**Gap:** The current check is binary (supplier / not supplier). The ROADMAP item asks for depth: bid history, active tenders, and awarded contract values. These three dimensions produce a much richer signal:
- Bid volume = how actively they pursue government contracts (higher volume → more compliance overhead, stronger KServe back-office pitch)
- Active tenders = current government procurement activity (signals cash flow from government side)
- Awarded contract values = scale of government business (large awarded values → strong compliance credential requirement, which is a direct KServe differentiator)

**gem.gov.in search capability:** The GeM portal has a public seller catalog and order search. Queries like `gem.gov.in/Home/SellerDetails?sellerId=[id]` or searching by company name in the GeM buyer/seller directory can surface these details. As a web search, the Worker can search `site:gem.gov.in "[company name]"` and look for seller profile pages.

---

## Conventions to Match

### Step structure pattern
Each step follows: NOTE preamble → instruction prose → **Sources (try in order)** → **Find:** bullets → **BD framing** rules → `Source(s): [URLs] | Confidence: HIGH/MED/LOW | Checked: YYYY-MM-DD`

### Output format template pattern
Each step has an emoji-prefixed block header (e.g., `💰 TURNOVER`, `👥 DIRECTORS`) with output fields beneath. New fields are appended to the existing block — they do not create separate blocks unless the content is fundamentally different (e.g., Regulatory Risk and Key Partnerships in Step 14 are separate enough to warrant their own sub-blocks).

### Checker criterion coverage
BD Relevance criterion (#7) currently covers: Steps 8, 10, 12, 14, 15, 16, 17. No changes to the Checker needed for these four items — they all fall within already-covered steps.

### Source Priority Reference table
Each step has a row. New content within an existing step updates the existing row. No new rows needed for these four items (all are extensions of Steps 3, 6, 7B, and 14).

### Wave assignments
- Step 3 → Wave 1. No change.
- Step 6 → Wave 1 (Step 6B is Wave 2). Board Composition Signal is Step 6 content → Wave 1. No wave change.
- Step 7B → Wave 1. No change.
- Step 14 → Wave 1. No change.

---

## Risks and Constraints

1. **GeM portal search reliability:** gem.gov.in is a government portal with variable search result quality. Worker must have a clear fallback instruction: if only binary presence/absence can be determined, report that and omit depth fields with `Unable to verify via public search`.

2. **Step 3 MCA multi-year access:** Tofler and Zauba Corp typically surface 2–3 years of financials. The Worker should attempt 3 years (FY24, FY23, FY22) and clearly note which years are available — not all private companies file consistently. If only 1 year is available, the trend classification should be `Insufficient data (only 1 year available)`.

3. **Board Composition Signal classification:** Classification must be based on designations from MCA only — not LinkedIn, not assumed from names. Clear classification rules are needed to prevent Worker interpretation errors:
   - Founder-dominated: MD/CEO/Promoter-Director holds > 50% of board seats AND is also a promoter/shareholder
   - Institutional: majority of board seats held by Independent Directors or PE/VC-nominated directors
   - Mixed: roughly equal split, or clear presence of both founder and institutional voices

4. **Attrition signal placement:** The keyword list and BD framing addition in Step 7B must not duplicate the existing "outsourcing pain" keywords — attrition signals are a distinct category and should be labeled as such to avoid conflation.
