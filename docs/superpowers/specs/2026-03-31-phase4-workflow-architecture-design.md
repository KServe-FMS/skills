# Phase 4 — Workflow & Architecture: Design Spec

**Date:** 2026-03-31
**Skill:** company-research
**Scope:** All 8 pending Phase 4 items from ROADMAP.md
**Approach:** Option A — inline protocol blocks added to existing sections

---

## Overview

This spec covers implementation of all 8 pending Phase 4 items. Each item is placed inline within the section where its enforcing role (Worker, Checker, Orchestrator) will read it. No new top-level sections are added.

---

## Item 1 — Tool Availability Detection

**Location:** Core Research Principles (after existing "Graceful degradation" block)

**Rule:** If a primary source for a step is unreachable — distinct from rate-limited or access-denied — explicitly try the secondary source from the Source Priority table before noting the gap. Only after the secondary also fails should the step note "Not publicly available." This prevents silent gaps from a single unreachable source when a working fallback exists.

---

## Item 2 — Source Failover Chain Automation

**Location:** Core Research Principles (replaces vague "switch to the next source" language in the rate-limited block)

**Rule:** Workers must traverse the Source Priority table mechanically: Primary → Secondary → Fallback, without returning to the user between attempts. Each failed attempt is noted in the report. Only after all three tiers fail does the step emit `RETRY_EXHAUSTED`. This converts the failover principle into a required execution path, not optional judgment.

---

## Item 3 — SEQUENTIAL → PARALLEL Auto-Upgrade Detection

**Location:** Platform Execution Mode (after the mode detection table)

**Rule:** Before starting any research run, test whether subagent tools (`Task`, `spawn_agent`, or platform equivalent) are available. If they are available and SEQUENTIAL was assumed or defaulted to, offer the user a choice:

```
⚡ Parallel mode available. I can run all 17 research steps simultaneously (~3× faster).
Continue in SEQUENTIAL (current), or switch to PARALLEL?
```

Wait for confirmation before proceeding. Never auto-switch without user confirmation. If the user doesn't respond or declines, continue in SEQUENTIAL.

---

## Item 4 — Dependency-Aware Wave Scheduling

**Location:** Platform Execution Mode — PARALLEL section (replaces existing Wave 1 / Wave 2 spawn instructions)

**Wave renumbering (waves only — research step numbers unchanged):**

| Wave | Steps | Spawn condition |
|---|---|---|
| Wave 1 | 2, 3, 4, 5, 6, 7, 7B, 7C, 8, 11, 12, 13, 14, 16, 17 (15 independent workers) | Spawn simultaneously after user confirms |
| Wave 2 | 6B, 9 (2 dependent workers) | Spawn after Wave 1 fully Checker-approved |
| Sanitizer gate | — | Run after Wave 2 complete |
| Wave 3 | 10, 10B (2 synthesis workers) | Spawn after Sanitizer complete |

**Total: 19 workers (15 + 2 + 2). Orchestrator worker count annotation: `19 = 15 Wave 1 + 2 Wave 2 + 2 Wave 3`.**

**Dependency rationale:**
- Step 6B depends on Step 6 (needs ★-flagged director list)
- Step 9 depends on Step 8 (synthesizes review data)
- Step 10B depends on Step 10 (already Wave 3, noted for completeness)

**Progress board update** (reflects new wave structure):
```
Research started for [Company Name]. Running 15 parallel Wave 1 workers:
⏳ In progress: Steps 2, 3, 4, 5, 6, 7, 7B, 7C, 8, 11, 12, 13, 14, 16, 17
⏸️  Waiting for Wave 1: Steps 6B, 9 (spawn after Wave 1 complete)
⏸️  Waiting for Sanitizer: Steps 10 & 10B (KServe Fit + ICP Score)
I'll update you as sections complete.
```

---

## Item 5 — Worker Output Schema Validation

**Location:** Checker Instructions (new pre-check gate, runs before the existing 8 criteria)

**Schema gate:** Before evaluating any criterion, verify minimum required structure:

| Required field | What to check |
|---|---|
| Data content | At least one data finding is present (not blank, not "TBD") |
| Source citation | At least one URL or document reference is present |
| Confidence label | A `HIGH / MED / LOW` label is present with a source justification |
| Step identifier | Output is clearly attributed to a specific step number |

If any required field is absent: return immediately to Worker with:
`Schema invalid — missing: [field name(s)]. Resubmit with all required fields present.`

Schema rejections do **not** count against the 2-retry budget. The retry budget applies only after schema passes.

---

## Item 6 — Orchestrator Completeness Health Check

**Location:** Orchestrator Instructions (replaces current informal steps 2–4 with a formal checklist)

**Pre-assembly checklist:**

| Check | Pass condition |
|---|---|
| All 19 Workers present | Outputs from Steps 2–9, 11–14, 16–17 (Wave 1) + Steps 6B, 9 (Wave 2) + Steps 10, 10B (Wave 3) all present |
| Wave sequencing correct | Wave 2 ran after Wave 1 fully complete; Wave 3 ran after Sanitizer complete |
| No pending steps | No step output is blank, "TBD", or "pending" without a ⚠️ flag or RETRY_EXHAUSTED signal |
| RETRY_EXHAUSTED collected | All exhausted-retry signals from Checkers are logged — none silently dropped |
| Sanitizer ran | Sanitizer gate completed between Wave 2 and Wave 3; security events line populated (even if "None") |

If any check fails: resolve before rendering. If a step is genuinely missing and cannot be recovered, add a ⚠️ note in its section and proceed.

---

## Item 7 — Partial-Run Resume Protocol

**Location:** Orchestrator Instructions (new block after the Health Check)

**Scope:** PARALLEL mode only. If interrupted mid-wave, the Orchestrator presents a resume summary:

```
⚠️ Previous run interrupted for [Company Name].
Completed: Steps [list] ✓
Incomplete: Steps [list] — need to re-run

Resume (re-run only incomplete steps) or Start fresh?
```

- **Resume:** Re-use all Checker-approved outputs. Spawn only incomplete Workers. Re-run Sanitizer and Wave 3 regardless — never re-use synthesis outputs from an interrupted run.
- **Start fresh:** Discard all prior outputs and run the full flow from Step 2.

If the platform does not support output persistence across sessions, skip resume detection and always run fresh.

---

## Item 8 — Idempotent Re-Run Support

**Location:** Research Flow — Phase 2 (new block at the start, before any Workers are spawned)

**Duplicate run detection:**

- Report exists, **< 24 hours old:** prompt user before re-running:
  ```
  ℹ️ A report for [Company Name] was already produced in this session ([time] ago).
  Use existing report or run fresh research?
  ```
  On **Use existing**: present prior report. On **Run fresh**: proceed normally and replace prior output.

- Report exists, **≥ 24 hours old:** run fresh automatically. Note at top of new report: `⚠️ Previous report from [date] superseded.`

- **No prior report:** proceed normally.

If the platform does not persist session history, skip this check and always run fresh.

---

## Cross-References Requiring Updates

When implementing, the following locations in SKILL.md reference old wave numbers and will need updating:

| Location | Current text | Update needed |
|---|---|---|
| Platform Execution Mode — PARALLEL | "Wave 1", "Wave 1.5", "Wave 2" spawn instructions | Rename to Wave 1 / Wave 2 / Sanitizer gate / Wave 3 |
| Orchestrator Instructions | "19 = 17 Wave 1 + 2 Wave 2" | "19 = 15 Wave 1 + 2 Wave 2 + 2 Wave 3" |
| Sanitizer Instructions | "Scan all approved Wave 1 outputs (Steps 2–9, 11–14, 16–17)" | Update to "Scan all approved Wave 1 + Wave 2 outputs (Steps 2–9, 6B, 11–14, 16–17 — 17 steps total)" — same 17 steps, now sourced from two waves |
| Source Priority table | Step 9 fallback row | Note dependency on Step 8 |
| Progress board template | Wave status lines | Update to reflect 4-stage flow |
| Architecture diagrams | Wave labels in ASCII diagrams | Update wave labels |

---

## Release Notes (for ROADMAP.md update)

All 8 Phase 4 items ship in this release. Mark the following as `[x]`:
- Tool Availability Detection
- Partial-Run Resume Protocol
- SEQUENTIAL → PARALLEL Auto-Upgrade Detection
- Source Failover Chain Automation
- Worker Output Schema Validation
- Dependency-Aware Wave Scheduling
- Idempotent Re-Run Support
- Orchestrator Completeness Health Check
