# Phase 4 — Workflow & Architecture Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Implement all 8 pending Phase 4 items in `company-research/SKILL.md`, then audit wave-number cross-references, update ROADMAP.md, bump the version, and push.

**Architecture:** All changes are inline additions or replacements within existing sections of `company-research/SKILL.md`. No new top-level sections. Research step numbers (6B, 7B, 7C, 10B) are NOT renumbered. Wave numbers are restructured from Wave 1 / Wave 1.5 / Wave 2 → Wave 1 / Wave 2 / Sanitizer gate / Wave 3.

**Tech Stack:** Markdown/YAML skill file. No build or test commands — verify edits by reading back changed sections.

---

## Files

- Modify: `company-research/SKILL.md` — all 8 Phase 4 items + cross-reference audit
- Modify: `ROADMAP.md` — mark 8 items shipped, bump current version
- Modify: `package.json` — bump version from 1.4.1 → 1.5.0

---

## Task 1: Add Tool Availability Detection to Core Research Principles

**File:** `company-research/SKILL.md` — after line ~142 (after "Graceful degradation" block)

- [ ] **Step 1: Add the new named block**

Find this exact text in `company-research/SKILL.md`:
```
**Graceful degradation.** If a tool or data source is unavailable, note it clearly in that section and move on. Never halt the entire report because one step hit a wall.

**Tool class unavailable.**
```

Replace with:
```
**Graceful degradation.** If a tool or data source is unavailable, note it clearly in that section and move on. Never halt the entire report because one step hit a wall.

**Tool availability detection.** If a primary source for a step is unreachable — distinct from rate-limited or access-denied — explicitly try the secondary source from the Source Priority table before noting the gap. Only after the secondary also fails should the step note "Not publicly available." This prevents silent gaps from a single unreachable source when a working fallback exists.

**Tool class unavailable.**
```

- [ ] **Step 2: Verify**

Read lines 140–150 of `company-research/SKILL.md` and confirm "Tool availability detection." block appears between "Graceful degradation." and "Tool class unavailable."

---

## Task 2: Mechanize Source Failover Chain in Core Research Principles

**File:** `company-research/SKILL.md` — replace the "Rate-limited or gated sources" block (~lines 150–159)

- [ ] **Step 1: Replace the rate-limited block**

Find this exact text:
```
**Rate-limited or gated sources.** If a source returns a 429, access-denied, or login-required response:
1. Do not retry the same source more than once immediately.
2. Switch to the next source in the Source Priority table for that step.
3. Note in the report: `⚠️ [Source name] access denied/rate-limited — [fallback source] used instead.`
4. If ALL sources for a step are gated: flag the step as `RETRY_EXHAUSTED` with reason "all sources gated" and move on without loop-retrying.
```

Replace with:
```
**Source failover chain.** Workers must traverse the Source Priority table mechanically — Primary → Secondary → Fallback — without returning to the user between attempts. Each failed attempt (whether unreachable, rate-limited, or access-denied) is noted in the report. Only after all three tiers fail does the step emit `RETRY_EXHAUSTED`.

For each failed source:
1. Do not retry the same source more than once immediately.
2. Advance to the next source in the Source Priority table.
3. Note in the report: `⚠️ [Source name] unavailable/rate-limited — [next source] used instead.`
4. If ALL sources for a step are exhausted: flag the step as `RETRY_EXHAUSTED` with reason "all sources exhausted" and move on.
```

- [ ] **Step 2: Verify**

Read lines 148–162 of `company-research/SKILL.md` and confirm "Source failover chain." block is present and the old "Rate-limited or gated sources." heading is gone.

- [ ] **Step 3: Commit**

```bash
git add company-research/SKILL.md
git commit -m "feat(skill): add tool availability detection and source failover chain (Phase 4)"
```

---

## Task 3: Add SEQUENTIAL → PARALLEL Auto-Upgrade Detection

**File:** `company-research/SKILL.md` — after "If unsure, default to **SEQUENTIAL** — it is always safe, just slower." (~line 56)

- [ ] **Step 1: Add the auto-upgrade detection block**

Find this exact text:
```
If unsure, default to **SEQUENTIAL** — it is always safe, just slower.

**PARALLEL:** Spawn in two waves after user confirms.
```

Replace with:
```
If unsure, default to **SEQUENTIAL** — it is always safe, just slower.

**Auto-upgrade detection.** Before starting any research run, test whether subagent tools (`Task`, `spawn_agent`, or platform equivalent) are available. If they are available and SEQUENTIAL was assumed or defaulted to, offer the user a choice before proceeding:

```
⚡ Parallel mode available. I can run all 17 research steps simultaneously (~3× faster).
Continue in SEQUENTIAL (current), or switch to PARALLEL?
```

Wait for confirmation. Never auto-switch without user confirmation. If the user doesn't respond or declines, continue in SEQUENTIAL.

**PARALLEL:** Spawn in three waves after user confirms.
```

- [ ] **Step 2: Verify**

Read lines 54–62 of `company-research/SKILL.md` and confirm "Auto-upgrade detection." block appears after the default-to-SEQUENTIAL line, and that "Spawn in three waves" is now the PARALLEL opener.

---

## Task 4: Rewrite PARALLEL Wave Structure (Wave Renumbering + Dependency-Aware Scheduling)

**File:** `company-research/SKILL.md` — replace the PARALLEL wave spawn block and progress reporting (~lines 58–77)

- [ ] **Step 1: Replace wave spawn instructions and progress board**

Find this exact text (after the "PARALLEL: Spawn in three waves" line you just wrote):
```
**Wave 1 — spawn simultaneously:** Workers 2, 3, 4, 5, 6, 6B, 7, 7B, 7C, 8, 9, 11, 12, 13, 14, 16, 17. Each Worker runs its own Checker loop independently.

**Wave 1.5 — Sanitizer gate (run after ALL Wave 1 workers are Checker-approved):** Before spawning Wave 2, run the Sanitizer across all approved Wave 1 outputs. See Sanitizer Instructions. Pass sanitized outputs to the Orchestrator.

**Wave 2 — spawn only after the Sanitizer gate is complete:** Workers 10 (KServe Fit) and 10B (ICP Score). Worker 10 reads the **sanitized** approved outputs from Steps 2–9. Worker 10B reads sanitized Steps 2–9, 11–14, and 16–17. Do not spawn Workers 10 or 10B until the Sanitizer has completed.

Orchestrator assembles the final report once Workers 10, 10B, and all Wave 1 workers are complete.

**PARALLEL — Progress reporting:** After spawning Wave 1, immediately post a status board to the user:
```
Research started for [Company Name]. Running 17 parallel workers:
⏳ In progress: Steps 2, 3, 4, 5, 6, 6B, 7, 7B, 7C, 8, 9, 11, 12, 13, 14, 16, 17
⏸️  Waiting to spawn: Steps 10 & 10B (KServe Fit + ICP Score — start after Wave 1 completes)
I'll update you as sections complete.
```
As each Worker is approved by its Checker, post a one-line update: `✓ [Step name] complete — [1-phrase summary, e.g., "Turnover: ₹847 Cr FY24"]`

When Wave 1 is fully complete: `Wave 1 complete. Running Sanitizer gate…` Then after Sanitizer completes: `Sanitizer complete. Spawning KServe Fit (Step 10) and ICP Score (Step 10B). Assembling final report…`
```

Replace with:
```
**Wave 1 — spawn simultaneously (15 independent workers):** Steps 2, 3, 4, 5, 6, 7, 7B, 7C, 8, 11, 12, 13, 14, 16, 17. Each Worker runs its own Checker loop independently.

**Wave 2 — spawn after Wave 1 fully Checker-approved (2 dependent workers):** Steps 6B (Decision-Maker Dossiers) and 9 (Rating). Step 6B depends on the ★-flagged director list from Step 6. Step 9 depends on the review data from Step 8. Spawn both simultaneously once Wave 1 is complete.

**Sanitizer gate — run after Wave 2 is fully Checker-approved:** Scan all approved Wave 1 + Wave 2 outputs (17 steps total). See Sanitizer Instructions. Pass sanitized outputs to the Orchestrator.

**Wave 3 — spawn only after the Sanitizer gate is complete (2 synthesis workers):** Steps 10 (KServe Fit) and 10B (ICP Score). Step 10 reads the **sanitized** approved outputs from Steps 2–9. Step 10B reads sanitized Steps 2–9, 11–14, and 16–17. Do not spawn Steps 10 or 10B until the Sanitizer has completed.

Orchestrator assembles the final report once all 19 Workers are complete (15 Wave 1 + 2 Wave 2 + 2 Wave 3).

**PARALLEL — Progress reporting:** After spawning Wave 1, immediately post a status board to the user:
```
Research started for [Company Name]. Running 15 parallel Wave 1 workers:
⏳ In progress: Steps 2, 3, 4, 5, 6, 7, 7B, 7C, 8, 11, 12, 13, 14, 16, 17
⏸️  Waiting for Wave 1: Steps 6B, 9 (spawn after Wave 1 complete)
⏸️  Waiting for Sanitizer: Steps 10 & 10B (KServe Fit + ICP Score)
I'll update you as sections complete.
```
As each Worker is approved by its Checker, post a one-line update: `✓ [Step name] complete — [1-phrase summary, e.g., "Turnover: ₹847 Cr FY24"]`

When Wave 1 is fully complete: `Wave 1 complete. Spawning Wave 2 (Steps 6B and 9)…` When Wave 2 is fully complete: `Wave 2 complete. Running Sanitizer gate…` Then after Sanitizer completes: `Sanitizer complete. Spawning KServe Fit (Step 10) and ICP Score (Step 10B). Assembling final report…`
```

- [ ] **Step 2: Verify**

Read lines 58–82 of `company-research/SKILL.md`. Confirm:
- "Wave 1" has 15 workers and does NOT list 6B or 9
- "Wave 2" lists Steps 6B and 9 with dependency rationale
- "Sanitizer gate" appears between Wave 2 and Wave 3
- "Wave 3" lists Steps 10 and 10B
- Progress board shows three ⏸️ lines
- Status messages say "Spawning Wave 2" and "Wave 2 complete"

- [ ] **Step 3: Commit**

```bash
git add company-research/SKILL.md
git commit -m "feat(skill): auto-upgrade detection and wave restructure 1/2/Sanitizer/3 (Phase 4)"
```

---

## Task 5: Add Idempotent Re-Run Support to Research Flow

**File:** `company-research/SKILL.md` — start of Phase 2, before "Run all 16 research steps" (~line 114)

- [ ] **Step 1: Insert duplicate run detection block**

Find this exact text:
```
### Phase 2 — Full Research (after user confirms)

Run all 16 research steps (Steps 2–17) using the execution mode detected above.
```

Replace with:
```
### Phase 2 — Full Research (after user confirms)

**Duplicate run detection.** Before spawning any Workers, check if a research report for this company was already produced in the current session:

- If a report exists and is **less than 24 hours old**: notify the user before re-running:
  ```
  ℹ️ A report for [Company Name] was already produced in this session ([time] ago).
  Use existing report or run fresh research?
  ```
  On **Use existing**: present the prior report. On **Run fresh**: proceed normally and replace the prior output.

- If a report exists but is **24 hours or older**: run fresh automatically. Note at the top of the new report: `⚠️ Previous report from [date] superseded.`

- If no prior report exists: proceed normally.

If the platform does not persist session history, skip this check and always run fresh.

Run all 16 research steps (Steps 2–17) using the execution mode detected above.
```

- [ ] **Step 2: Verify**

Read lines 112–125 of `company-research/SKILL.md` and confirm the "Duplicate run detection." block appears immediately after the Phase 2 heading and before "Run all 16 research steps."

- [ ] **Step 3: Commit**

```bash
git add company-research/SKILL.md
git commit -m "feat(skill): idempotent re-run support with duplicate run detection (Phase 4)"
```

---

## Task 6: Add Worker Output Schema Gate to Checker Instructions

**File:** `company-research/SKILL.md` — before "When validating any Worker output, apply all eight criteria:" (~line 1099)

- [ ] **Step 1: Insert schema gate block**

Find this exact text:
```
## Checker Instructions

When validating any Worker output, apply all eight criteria:
```

Replace with:
```
## Checker Instructions

**Schema gate (run before the 8 criteria).** Before evaluating any criterion, verify the Worker output has the minimum required structure:

| Required field | What to check |
|---|---|
| Data content | At least one data finding is present (not blank, not "TBD") |
| Source citation | At least one URL or document reference is present |
| Confidence label | A `HIGH / MED / LOW` label is present with a source justification |
| Step identifier | Output is clearly attributed to a specific step number |

If any required field is absent: return immediately to Worker with:
`Schema invalid — missing: [field name(s)]. Resubmit with all required fields present.`

Schema rejections do **not** count against the 2-retry budget. The retry budget applies only after schema passes.

When validating any Worker output, apply all eight criteria:
```

- [ ] **Step 2: Verify**

Read the Checker Instructions section opening. Confirm the schema gate table appears before the "1. Source present?" criterion list.

- [ ] **Step 3: Commit**

```bash
git add company-research/SKILL.md
git commit -m "feat(skill): worker output schema gate in Checker Instructions (Phase 4)"
```

---

## Task 7: Update Sanitizer Instructions for New Wave Structure

**File:** `company-research/SKILL.md` — Sanitizer Instructions section (~lines 1140–1165)

- [ ] **Step 1: Update Sanitizer header line**

Find:
```
The Sanitizer runs once as a Wave 1.5 gate before Wave 2 spawns.
```

Replace with:
```
The Sanitizer runs once as a gate between Wave 2 and Wave 3.
```

- [ ] **Step 2: Update PARALLEL mode trigger**

Find:
```
- **PARALLEL mode:** after all Wave 1 Workers are Checker-approved, before spawning Workers 10 and 10B
```

Replace with:
```
- **PARALLEL mode:** after all Wave 2 Workers (Steps 6B and 9) are Checker-approved, before spawning Wave 3 Workers (Steps 10 and 10B)
```

- [ ] **Step 3: Update "What to scan" line**

Find:
```
**What to scan:** All approved Wave 1 outputs (Steps 2–9, 11–14, 16–17 — 17 steps total). Note: Step 9's output is a synthesized artifact (scored summary of Step 8 data), not raw third-party content — the scan applies equally but may find lower injection surface.
```

Replace with:
```
**What to scan:** All approved Wave 1 + Wave 2 outputs (Steps 2–9, 6B, 11–14, 16–17 — 17 steps total). Note: Step 9's output is a synthesized artifact (scored summary of Step 8 data), not raw third-party content — the scan applies equally but may find lower injection surface.
```

- [ ] **Step 4: Update step 5 of Sanitizer instructions**

Find:
```
5. Pass sanitized outputs to Orchestrator. Orchestrator spawns Wave 2 Workers (Steps 10, 10B) using these sanitized outputs only.
```

Replace with:
```
5. Pass sanitized outputs to Orchestrator. Orchestrator spawns Wave 3 Workers (Steps 10, 10B) using these sanitized outputs only.
```

- [ ] **Step 5: Verify**

Read the full Sanitizer Instructions section. Confirm all four references to old wave numbers are updated and the section is internally consistent.

- [ ] **Step 6: Commit**

```bash
git add company-research/SKILL.md
git commit -m "feat(skill): update Sanitizer Instructions for Wave 1/2/Sanitizer/3 structure (Phase 4)"
```

---

## Task 8: Rewrite Orchestrator Instructions — Health Check + Resume Protocol

**File:** `company-research/SKILL.md` — Orchestrator Instructions section (~lines 1168–1179)

- [ ] **Step 1: Replace Orchestrator Instructions opening and steps 1–7**

Find this exact text:
```
## Orchestrator Instructions

After all 19 Workers complete and each Checker has approved (19 = 17 Wave 1 Workers [Steps 2–9, 11–14, 16–17] + 2 Wave 2 Workers [Steps 10 + 10B]):

1. Assemble all approved sections into the Output Format template in order
2. **Before assembling Steps 10 & 10B (KServe Fit + ICP Score):** verify that the Sanitizer gate has completed and that approved **sanitized** outputs from ALL of Steps 2–9 are present. If any Wave 1 step is still pending or the Sanitizer has not run, wait. If a Step 10 or 10B Worker ran before the Sanitizer completed, discard that output and re-request with the full sanitized Wave 1 context.
3. Validate: no field is blank, pending, or "TBD" without a "Not publicly available" statement or a ⚠️ flag
4. If any section is missing or incomplete, return to that step's Checker with a re-request before rendering
5. Collect all `RETRY_EXHAUSTED` signals received from Checkers. If any exist, populate the "Data gaps" line in the 📝 DATA QUALITY footer with: `[Step N — field] — [reason]` for each one. If none, write "None".
   Separately, collect all `INJECTION_FLAGGED` signals from Checkers and any "Sanitizer stripped" entries from the Sanitizer. Populate the **Security events** line in the DATA QUALITY footer: list each as `INJECTION_FLAGGED: [Step N — platform]` or `Sanitizer stripped: [Step N — platform]`. If none, write "None".
6. Tally confidence levels across all 16 sections and populate the "Overall" line in the DATA QUALITY footer (e.g., `9/16 HIGH · 5 MED · 2 LOW`). Find the oldest source date across all sections and populate "Oldest source".
7. Render the final report for presentation to the user
```

Replace with:
```
## Orchestrator Instructions

After all 19 Workers complete and each Checker has approved (19 = 15 Wave 1 Workers [Steps 2, 3, 4, 5, 6, 7, 7B, 7C, 8, 11, 12, 13, 14, 16, 17] + 2 Wave 2 Workers [Steps 6B + 9] + 2 Wave 3 Workers [Steps 10 + 10B]):

**Pre-assembly completeness checklist.** Before assembling the final report, verify all of the following:

| Check | Pass condition |
|---|---|
| All 19 Workers present | Outputs from Wave 1 (Steps 2, 3, 4, 5, 6, 7, 7B, 7C, 8, 11, 12, 13, 14, 16, 17) + Wave 2 (Steps 6B, 9) + Wave 3 (Steps 10, 10B) all present |
| Wave sequencing correct | Wave 2 ran after Wave 1 fully complete; Wave 3 ran after Sanitizer complete |
| No pending steps | No step output is blank, "TBD", or "pending" without a ⚠️ flag or RETRY_EXHAUSTED signal |
| RETRY_EXHAUSTED collected | All exhausted-retry signals from Checkers are logged — none silently dropped |
| Sanitizer ran | Sanitizer gate completed between Wave 2 and Wave 3; security events line populated (even if "None") |

If any check fails: resolve before rendering. If a step is genuinely missing and cannot be recovered, add a ⚠️ note in its section and proceed.

1. Assemble all approved sections into the Output Format template in order
2. **Before assembling Steps 10 & 10B (KServe Fit + ICP Score):** verify the Sanitizer gate completed and sanitized outputs from ALL of Steps 2–9 are present. If Wave 3 Workers ran before the Sanitizer completed, discard those outputs and re-request with the full sanitized context.
3. Validate: no field is blank, pending, or "TBD" without a "Not publicly available" statement or a ⚠️ flag
4. If any section is missing or incomplete, return to that step's Checker with a re-request before rendering
5. Collect all `RETRY_EXHAUSTED` signals received from Checkers. If any exist, populate the "Data gaps" line in the 📝 DATA QUALITY footer with: `[Step N — field] — [reason]` for each one. If none, write "None".
   Separately, collect all `INJECTION_FLAGGED` signals from Checkers and any "Sanitizer stripped" entries from the Sanitizer. Populate the **Security events** line in the DATA QUALITY footer: list each as `INJECTION_FLAGGED: [Step N — platform]` or `Sanitizer stripped: [Step N — platform]`. If none, write "None".
6. Tally confidence levels across all 16 sections and populate the "Overall" line in the DATA QUALITY footer (e.g., `9/16 HIGH · 5 MED · 2 LOW`). Find the oldest source date across all sections and populate "Oldest source".
7. Render the final report for presentation to the user

**Partial-run resume (PARALLEL mode only).** If a PARALLEL run is interrupted mid-wave — connection drop, timeout, platform restart — present the user with a resume summary before restarting:

```
⚠️ Previous run interrupted for [Company Name].
Completed: Steps [list] ✓
Incomplete: Steps [list] — need to re-run

Resume (re-run only incomplete steps) or Start fresh?
```

- **Resume:** Re-use all Checker-approved outputs from the interrupted run. Spawn only the incomplete Workers. Re-run the Sanitizer gate and Wave 3 regardless — never re-use synthesis outputs from an interrupted run.
- **Start fresh:** Discard all prior outputs and run the full flow from Step 2.

If the platform does not support output persistence across sessions, skip resume detection and always run fresh.
```

- [ ] **Step 2: Verify**

Read the full Orchestrator Instructions section. Confirm:
- Opening annotation says "19 = 15 Wave 1 + 2 Wave 2 + 2 Wave 3"
- Completeness checklist table is present with 5 rows
- Steps 1–7 follow the checklist
- Step 2 says "Wave 3 Workers" not "Wave 2 Workers"
- Partial-run resume protocol is present at the end

- [ ] **Step 3: Commit**

```bash
git add company-research/SKILL.md
git commit -m "feat(skill): orchestrator completeness health check and partial-run resume (Phase 4)"
```

---

## Task 9: Update Multi-Agent Architecture ASCII Diagram

**File:** `company-research/SKILL.md` — PARALLEL MODE diagram (~lines 1030–1067)

- [ ] **Step 1: Replace the PARALLEL MODE ASCII diagram**

Find this exact text:
```
### PARALLEL MODE

```
User confirms company (Step 1)
         │
         ▼ POST PROGRESS STATUS BOARD
┌─────────────────────────────────────────────────────┐
│    WAVE 1 — SPAWN SIMULTANEOUSLY                    │
│  Workers: 2, 3, 4, 5, 6, 6B, 7, 7B, 7C             │
│           8, 9*, 11, 12, 13, 14, 16, 17             │
│  (*Step 9 waits for Step 8 internally)              │
│  Post ✓ update after each worker approved           │
└─────────────────────────────────────────────────────┘
         │ (each worker ↔ checker loop — 8 criteria)
         ▼ POST "Wave 1 complete. Running Sanitizer gate…"
┌─────────────────────────────────────────────────────┐
│    WAVE 1.5 — SANITIZER GATE                        │
│  Scans all approved Wave 1 outputs                  │
│  Strips injection patterns                          │
│  Logs Security events in DATA QUALITY footer        │
└─────────────────────────────────────────────────────┘
         ▼ POST "Sanitizer complete. Spawning Steps 10 & 10B…"
┌─────────────────────────────────────────────────────┐
│    WAVE 2 — SPAWN AFTER SANITIZER COMPLETE          │
│  Workers: 10 (KServe Fit), 10B (ICP Score)          │
│  Worker 10:  sanitized Steps 2–9                    │
│  Worker 10B: sanitized Steps 2–9, 11–14, 16–17      │
└─────────────────────────────────────────────────────┘
         │ (Wave 2 ↔ checker loop)
         ▼
┌─────────────────────────────────────────────────────┐
│         ORCHESTRATOR                                │
│  Verify Steps 10 & 10B ran after Sanitizer complete │
│  Assemble all approved sections in order            │
│  Validate completeness · Tally confidence           │
│  Collect RETRY_EXHAUSTED signals → Data gaps        │
│  Collect INJECTION_FLAGGED + Sanitizer → Security   │
│  Render final BD Research Report                    │
└─────────────────────────────────────────────────────┘
```
```

Replace with:
```
### PARALLEL MODE

```
User confirms company (Step 1)
         │
         ▼ POST PROGRESS STATUS BOARD
┌─────────────────────────────────────────────────────┐
│    WAVE 1 — SPAWN SIMULTANEOUSLY (15 workers)       │
│  Workers: 2, 3, 4, 5, 6, 7, 7B, 7C, 8              │
│           11, 12, 13, 14, 16, 17                    │
│  Post ✓ update after each worker approved           │
└─────────────────────────────────────────────────────┘
         │ (each worker ↔ checker loop — schema gate + 8 criteria)
         ▼ POST "Wave 1 complete. Spawning Wave 2…"
┌─────────────────────────────────────────────────────┐
│    WAVE 2 — SPAWN AFTER WAVE 1 COMPLETE (2 workers) │
│  Worker 6B: Decision-Maker Dossiers (needs Step 6)  │
│  Worker 9:  Rating (needs Step 8)                   │
└─────────────────────────────────────────────────────┘
         │ (Wave 2 ↔ checker loop)
         ▼ POST "Wave 2 complete. Running Sanitizer gate…"
┌─────────────────────────────────────────────────────┐
│    SANITIZER GATE                                   │
│  Scans all approved Wave 1 + Wave 2 outputs         │
│  (17 steps total)                                   │
│  Strips injection patterns                          │
│  Logs Security events in DATA QUALITY footer        │
└─────────────────────────────────────────────────────┘
         ▼ POST "Sanitizer complete. Spawning Steps 10 & 10B…"
┌─────────────────────────────────────────────────────┐
│    WAVE 3 — SPAWN AFTER SANITIZER COMPLETE          │
│  Workers: 10 (KServe Fit), 10B (ICP Score)          │
│  Worker 10:  sanitized Steps 2–9                    │
│  Worker 10B: sanitized Steps 2–9, 11–14, 16–17      │
└─────────────────────────────────────────────────────┘
         │ (Wave 3 ↔ checker loop)
         ▼
┌─────────────────────────────────────────────────────┐
│         ORCHESTRATOR                                │
│  Run completeness health check (5-point checklist)  │
│  Assemble all approved sections in order            │
│  Validate completeness · Tally confidence           │
│  Collect RETRY_EXHAUSTED signals → Data gaps        │
│  Collect INJECTION_FLAGGED + Sanitizer → Security   │
│  Render final BD Research Report                    │
└─────────────────────────────────────────────────────┘
```
```

- [ ] **Step 2: Verify**

Read the Multi-Agent Architecture section. Confirm:
- Wave 1 box shows 15 workers and does NOT list 6B or 9
- Wave 2 box shows Steps 6B and 9 with dependency notes
- "SANITIZER GATE" box (no wave number) appears between Wave 2 and Wave 3
- Wave 3 box shows Steps 10 and 10B
- Orchestrator box mentions "completeness health check"

- [ ] **Step 3: Commit**

```bash
git add company-research/SKILL.md
git commit -m "feat(skill): update Multi-Agent Architecture diagram for new wave structure (Phase 4)"
```

---

## Task 10: Review Pass — Audit All Remaining Wave Cross-References

**File:** `company-research/SKILL.md`

- [ ] **Step 1: Search for remaining stale wave references**

Run the following searches and note every location found:
```bash
grep -n "Wave 1.5\|Wave 2 Workers\|two waves\|17 parallel workers\|Wave 1 Workers\|6B.*Wave 1\|Step 9.*Wave 1" company-research/SKILL.md
```

- [ ] **Step 2: Fix any stale references found**

For each match found in Step 1, apply the appropriate fix:
- "Wave 1.5" → "Sanitizer gate"
- "Wave 2 Workers" (referring to Steps 10/10B) → "Wave 3 Workers"
- "two waves" → "three waves"
- "17 parallel workers" → "15 parallel Wave 1 workers"
- Any mention of 6B or 9 as Wave 1 workers → update to Wave 2

If grep returns no matches, this step is complete — proceed to Step 3.

- [ ] **Step 3: Search for SEQUENTIAL mode references that need updating**

```bash
grep -n "Wave 1\|Wave 2\|Sanitizer" company-research/SKILL.md | grep -v "^[[:space:]]*#"
```

Review each match in context (read surrounding 3 lines) to confirm SEQUENTIAL mode text is still accurate. SEQUENTIAL mode uses the same Sanitizer gate logic but runs it after Step 9 — this should not have changed.

- [ ] **Step 4: Verify Sanitizer Instructions "What to scan" step count**

Read the Sanitizer Instructions "What to scan" line. Confirm it says "Wave 1 + Wave 2 outputs (Steps 2–9, 6B, 11–14, 16–17 — 17 steps total)". Count the steps listed: 2, 3, 4, 5, 6, 7, 7B, 7C, 8, 9, 6B, 11, 12, 13, 14, 16, 17 = 17 ✓

- [ ] **Step 5: Commit if any fixes were made**

```bash
git add company-research/SKILL.md
git commit -m "fix(skill): wave cross-reference audit — clean up stale wave labels (Phase 4 review)"
```

If no fixes were needed, skip this commit.

---

## Task 11: Update ROADMAP.md — Mark 8 Items Shipped

**File:** `ROADMAP.md`

- [ ] **Step 1: Mark all 8 Phase 4 items as shipped**

In `ROADMAP.md`, find each of the following lines and change `- [ ]` to `- [x]`, adding `*(shipped: Phase 4 — 2026-03-31)*` at the end of each:

1. `- [ ] **Tool Availability Detection**`
2. `- [ ] **Partial-Run Resume Protocol**`
3. `- [ ] **SEQUENTIAL → PARALLEL Auto-Upgrade Detection**`
4. `- [ ] **Source Failover Chain Automation**`
5. `- [ ] **Worker Output Schema Validation**`
6. `- [ ] **Dependency-Aware Wave Scheduling**`
7. `- [ ] **Idempotent Re-Run Support**`
8. `- [ ] **Orchestrator Completeness Health Check**`

- [ ] **Step 2: Update the Phase 4 heading**

Find:
```
## Phase 4 — Workflow & Architecture
```

Replace with:
```
## Phase 4 — Workflow & Architecture ✅ COMPLETE (shipped in v1.5.0 — 2026-03-31)
```

- [ ] **Step 3: Update current skill version at the top of the file**

Find:
```
**Current skill version:** v1.4.0
```

Replace with:
```
**Current skill version:** v1.5.0
```

Note: if the file already shows v1.4.1, replace that instead.

- [ ] **Step 4: Verify**

Read the Phase 4 section of ROADMAP.md. Confirm all 8 items show `[x]` and the heading shows ✅ COMPLETE.

---

## Task 12: Bump Version in package.json

**File:** `package.json`

- [ ] **Step 1: Bump version**

Find:
```
"version": "1.4.1",
```

Replace with:
```
"version": "1.5.0",
```

- [ ] **Step 2: Verify**

Read `package.json` and confirm version is `1.5.0`.

---

## Task 13: Final Commit, Tag, and Push

- [ ] **Step 1: Commit ROADMAP and package.json together**

```bash
git add ROADMAP.md package.json
git commit -m "chore(release): v1.5.0"
```

- [ ] **Step 2: Tag the release**

```bash
git tag v1.5.0
```

- [ ] **Step 3: Push branch and tags**

```bash
git push && git push --tags
```

- [ ] **Step 4: Verify**

```bash
git log --oneline -5
git tag --list | tail -5
```

Confirm `v1.5.0` tag is present and the chore(release) commit is the most recent.
