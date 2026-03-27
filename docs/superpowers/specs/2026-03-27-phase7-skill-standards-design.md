# Phase 7 — Skill Standards & Quality: Design Spec
**Date:** 2026-03-27
**Skill:** `company-research/SKILL.md`
**Source:** ROADMAP.md Phase 7 (12 items from skill-creator audit)

---

## Overview

All 12 Phase 7 items are surgical corrections to `company-research/SKILL.md`. No new research steps, no new output sections. Changes fall into four groups implemented as discrete tasks.

---

## Group 1 — Description rewrite + Compatibility statement

### Item 1 — YAML Trigger Description Precision

**Problem:** The 7-line `description` field opens with "Comprehensive BD intelligence research skill…" and buries triggering phrases as examples near the end. Per skill-creator guidance, descriptions should lead with when-to-trigger and use pushy language to combat undertriggering.

**Target users:** Non-technical sales reps who phrase requests naturally ("check out this company", "who should I call at X").

**Fix — replace the full `description` value with:**

```yaml
description: >
  Trigger this skill any time someone drops a company name in a sales or BD context — even
  if they don't say "research". Phrases like "check out [company]", "who should I call at
  [company]", "what do we know about [company]", "look up [company]", "get me a profile on
  [company]", or simply naming a company while discussing a prospect or outreach plan. Don't
  wait for an explicit request — if the context is prospecting, account intelligence, pre-call
  prep, or finding potential outsourcing clients for KServe, trigger immediately. Produces a
  full BD intelligence report: company size, financials, directors, reviews, ICP score, and a
  next-best-action recommendation.
```

### Item 12 — Compatibility Statement Update

**Problem:** The compatibility line omits modern platforms (Claude Desktop, Cursor, VS Code Agent).

**Current:** `Claude.ai · Claude Code · Cowork · OpenCode · Codex · Any AI agent platform`

**Fix:** `Claude.ai · Claude Code · Claude Desktop (MCP) · Cowork · OpenCode · Codex · Cursor · VS Code Agent · Any AI agent platform`

---

## Group 2 — Structural / dependency fixes

### Item 2 — Step 1 Explicit Numbering

**Problem:** `## Research Steps` header says `(Steps 2–17)` and jumps straight to `### Step 2`. Step 1 exists only as prose in the Research Flow section, creating an off-by-one in all cross-references.

**Fix:**
- Change section header: `## Research Steps (Steps 2–17)` → `## Research Steps (Steps 1–17)`
- Add before `### Step 2`, a new heading:

```markdown
### Step 1 — Company Verification

See **Research Flow — Phase 1 Verification** above.
```

No content duplication — just the heading and a pointer.

### Item 3 — Step 6B Source Priority Table Row

**Problem:** The Fallback column for Step 6B contains an instruction ("Mark Lines 2–3 as 'Not accessible' if LinkedIn profile is private") rather than a fallback source. Every other row names actual sources. The instruction already lives in the Step 6B body (line 258) and doesn't belong in the table.

**Current:**
```
| 6B — Dossiers | LinkedIn profiles of ★-flagged directors | Company website bio · News/conference mentions | Mark Lines 2–3 as "Not accessible" if LinkedIn profile is private |
```

**Fix:**
```
| 6B — Dossiers | LinkedIn profiles of ★-flagged directors | Company website bio · News/conference mentions | Conference speaking history · Industry press mentions |
```

### Item 4 — Step 10B Dependency Declaration Fix

**Problem:** Step 10B preamble says `Depends on: Steps 2–10`. The ICP Score dimensions explicitly draw from Step 12 (social presence dimension) and Step 14 (growth/change signal dimension), making the declaration factually incomplete.

**Current:** `**Depends on:** Steps 2–10 (all prior research).`

**Fix:** `**Depends on:** Steps 2–14 (all prior research — ICP dimensions draw from Step 12 and Step 14).`

### Item 6 — Step 15 Dependency Clarification

**Problem:** Step 15 says "Synthesize findings from Steps 2–17". Step 15 itself is within that range — a circular reference.

**Current:** `Synthesize findings from Steps 2–17 into actionable outreach intel.`

**Fix:** `Synthesize findings from Steps 2–14, 16, and 17 into actionable outreach intel.`

### Item 7 — Wave 2 Read-Scope Correction

**Problem:** The architecture diagram shows both Workers 10 and 10B reading `sanitized approved outputs from Steps 2–9`. Worker 10B's ICP dimensions require Steps 12 and 14, which are Wave 1 outputs outside the 2–9 range.

**Current (in PARALLEL mode architecture diagram):**
```
│  Read sanitized approved outputs from Steps 2–9     │
```

**Fix:** Replace with two explicit read-scope lines:
```
│  Worker 10:  reads sanitized outputs from Steps 2–9              │
│  Worker 10B: reads sanitized outputs from Steps 2–9, 11–14, 16–17│
```

---

## Group 3 — Annotation / scope fixes

### Item 5 — Checker Criterion #7 Scope Update

**Problem:** Criterion #7 (BD relevance) scope lists `Steps 8, 10, 12, 14, and 15`. Steps 16 and 17 both have explicit BD framing rules in their bodies — the Checker has no enforcement hook for them.

**Current:** `This criterion applies most strictly to Steps 8, 10, 12, 14, and 15.`

**Fix:** `This criterion applies most strictly to Steps 8, 10, 12, 14, 15, 16, and 17.`

### Item 8 — Orchestrator Worker Count Annotation

**Problem:** Orchestrator Instructions say "After all 19 Workers complete" with no explanation of how 19 is derived. Anyone adding or removing a step cannot verify the count.

**Current:** `After all 19 Workers complete and each Checker has approved:`

**Fix:** `After all 19 Workers complete and each Checker has approved (19 = 17 Wave 1 Workers [Steps 2–9, 11–14, 16–17] + 2 Wave 2 Workers [Steps 10 + 10B]):`

### Item 9 — Sanitizer Scope Explicit Listing

**Problem:** Sanitizer Instructions say "What to scan: All approved Wave 1 outputs." The step list is implicit — workers must infer it.

**Current:** `**What to scan:** All approved Wave 1 outputs.`

**Fix:** `**What to scan:** All approved Wave 1 outputs (Steps 2–9, 11–14, 16–17 — 17 steps total).`

---

## Group 4 — New content

### Item 10 — Platform Execution Mode Table Update

**Problem:** The SEQUENTIAL row only lists `Claude.ai · Cowork · Codex chat`. Users on Cursor, VS Code Agent, Claude Desktop, Cline, Continue.dev, and Windsurf have no explicit guidance and silently default to SEQUENTIAL without knowing it.

**Current SEQUENTIAL row:**
```
| **SEQUENTIAL** | Single-thread only — one step at a time | Claude.ai · Cowork · Codex chat · Any single-thread assistant |
```

**Fix:**
```
| **SEQUENTIAL** | Single-thread only — one step at a time | Claude.ai · Claude Desktop (MCP) · Cowork · Codex chat · Cursor · VS Code Agent · Cline · Continue.dev · Windsurf · Any single-thread assistant |
```

All added platforms are single-thread environments that do not support the `Task` tool or equivalent subagent spawning.

### Item 11 — Tool Absence Degradation Protocol

**Problem:** Core Research Principles covers rate-limited/gated sources but has no protocol for when an entire tool class (web search, file write, subagents) is simply absent. Without this, the skill silently attempts to proceed and produces incomplete results.

**Fix:** Add a new principle immediately after the existing `Graceful degradation` paragraph:

```markdown
**Tool class unavailable.** If a required tool class is entirely absent from the executing
environment — not rate-limited or gated, but simply not available — halt before starting
and notify the user:

> ⚠️ Required tool missing: [web search / file write / subagents]. This skill cannot produce
> a reliable report without it. Please check your platform configuration or switch to a
> supported environment (see Platform Execution Mode table above).

Do not attempt to proceed in a partially capable environment. An incomplete report handed
to BD is actively harmful.
```

---

## What is NOT changing

- No changes to research step content (Steps 2–17 bodies)
- No changes to output format template
- No changes to Checker criteria 1–6 or 8
- No changes to Sanitizer logic
- No new steps added

---

## File affected

`company-research/SKILL.md` — one file, 12 targeted edits.
