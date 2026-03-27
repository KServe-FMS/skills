# Phase 7 — Skill Standards & Quality Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Apply all 12 Phase 7 audit corrections to `company-research/SKILL.md` — fixing the YAML trigger description, dependency declarations, scope annotations, platform table, and adding a tool-absence protocol.

**Architecture:** One file (`company-research/SKILL.md`), 12 independent surgical text edits grouped into 4 tasks. No new research steps, no output format changes, no logic changes. Each task verifies before editing and verifies after.

**Tech Stack:** Markdown/YAML — Edit tool only. No build, test, or lint commands exist in this repo.

---

## Task 1: Description rewrite + Compatibility statement (Items 1 & 12)

**Files:**
- Modify: `company-research/SKILL.md:3-9` (YAML description)
- Modify: `company-research/SKILL.md:16` (compatibility line)

- [ ] **Step 1: Verify current description text**

Run:
```bash
grep -n "Comprehensive BD intelligence" company-research/SKILL.md
```
Expected: line 4 — `  Comprehensive BD intelligence research skill for KServe's business development team.`

- [ ] **Step 2: Replace YAML description**

In `company-research/SKILL.md`, replace:
```
description: >
  Comprehensive BD intelligence research skill for KServe's business development team.
  Use this skill whenever a user provides a company name (and optionally a website or address)
  and wants to research that company as a potential outsourcing client. Triggers on phrases like
  "research [company]", "look up [company]", "get me info on [company]", "do a BD profile for [company]",
  "check out this company", or any request to investigate a prospect company for sales or outreach purposes.
  Always use this skill when the context is about finding potential clients for KServe's BPO services.
```
With:
```
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

- [ ] **Step 3: Verify description updated**

Run:
```bash
grep -n "Trigger this skill" company-research/SKILL.md
```
Expected: line 3 or 4 — `  Trigger this skill any time someone drops a company name...`

- [ ] **Step 4: Verify current compatibility line**

Run:
```bash
grep -n "Compatible with" company-research/SKILL.md
```
Expected: one line containing `Claude.ai · Claude Code · Cowork · OpenCode · Codex · Any AI agent platform`

- [ ] **Step 5: Update compatibility statement**

In `company-research/SKILL.md`, replace:
```
**Compatible with:** Claude.ai · Claude Code · Cowork · OpenCode · Codex · Any AI agent platform
```
With:
```
**Compatible with:** Claude.ai · Claude Code · Claude Desktop (MCP) · Cowork · OpenCode · Codex · Cursor · VS Code Agent · Any AI agent platform
```

- [ ] **Step 6: Verify compatibility updated**

Run:
```bash
grep -n "Compatible with" company-research/SKILL.md
```
Expected: line contains `Claude Desktop (MCP)` and `Cursor · VS Code Agent`

- [ ] **Step 7: Commit**

```bash
git add company-research/SKILL.md
git commit -m "fix(skill): rewrite YAML trigger description and update compatibility statement

Phase 7 items 1 & 12 — description now leads with trigger signal using
pushy language for non-technical sales users; compatibility statement
adds Claude Desktop (MCP), Cursor, VS Code Agent."
```

---

## Task 2: Structural / dependency fixes (Items 2, 3, 4, 6, 7)

**Files:**
- Modify: `company-research/SKILL.md` — 5 edits across Research Steps header, Source Priority table, Step 10B preamble, Step 15 preamble, and Wave 2 architecture diagram

- [ ] **Step 1: Verify Research Steps header**

Run:
```bash
grep -n "Research Steps (Steps 2" company-research/SKILL.md
```
Expected: one line — `## Research Steps (Steps 2–17)`

- [ ] **Step 2: Fix Research Steps header and add Step 1 heading (Item 2)**

In `company-research/SKILL.md`, replace:
```
## Research Steps (Steps 2–17)

### Step 2 — Line of Business
```
With:
```
## Research Steps (Steps 1–17)

### Step 1 — Company Verification

See **Research Flow — Phase 1 Verification** above.

---

### Step 2 — Line of Business
```

- [ ] **Step 3: Verify Step 1 heading added**

Run:
```bash
grep -n "Step 1 — Company Verification" company-research/SKILL.md
```
Expected: one match in the Research Steps section

- [ ] **Step 4: Verify Step 6B table row current state**

Run:
```bash
grep -n "6B — Dossiers" company-research/SKILL.md
```
Expected: one line containing `Mark Lines 2–3 as "Not accessible" if LinkedIn profile is private`

- [ ] **Step 5: Fix Step 6B Source Priority table Fallback column (Item 3)**

In `company-research/SKILL.md`, replace:
```
| 6B — Dossiers | LinkedIn profiles of ★-flagged directors | Company website bio · News/conference mentions | Mark Lines 2–3 as "Not accessible" if LinkedIn profile is private |
```
With:
```
| 6B — Dossiers | LinkedIn profiles of ★-flagged directors | Company website bio · News/conference mentions | Conference speaking history · Industry press mentions |
```

- [ ] **Step 6: Verify Step 6B table row fixed**

Run:
```bash
grep -n "6B — Dossiers" company-research/SKILL.md
```
Expected: line now contains `Conference speaking history · Industry press mentions`

- [ ] **Step 7: Verify Step 10B dependency current state**

Run:
```bash
grep -n "Depends on.*Steps 2" company-research/SKILL.md
```
Expected: one match containing `Steps 2–10 (all prior research)`

- [ ] **Step 8: Fix Step 10B dependency declaration (Item 4)**

In `company-research/SKILL.md`, replace:
```
**Depends on:** Steps 2–10 (all prior research). In PARALLEL mode, run this step alongside Worker 10 (Wave 2), but only after Wave 1 is complete. In SEQUENTIAL mode, run after Step 10 is approved.
```
With:
```
**Depends on:** Steps 2–14 (all prior research — ICP dimensions draw from Step 12 and Step 14). In PARALLEL mode, run this step alongside Worker 10 (Wave 2), but only after Wave 1 is complete. In SEQUENTIAL mode, run after Step 10 is approved.
```

- [ ] **Step 9: Verify Step 10B dependency fixed**

Run:
```bash
grep -n "Depends on.*Steps 2" company-research/SKILL.md
```
Expected: line now contains `Steps 2–14`

- [ ] **Step 10: Verify Step 15 circular reference current state**

Run:
```bash
grep -n "Synthesize findings from Steps 2–17" company-research/SKILL.md
```
Expected: one match in the Step 15 section

- [ ] **Step 11: Fix Step 15 circular reference (Item 6)**

In `company-research/SKILL.md`, replace:
```
**Most important step.** Synthesize findings from Steps 2–17 into actionable outreach intel. **Do not run new web searches** — use only what was gathered in prior steps.
```
With:
```
**Most important step.** Synthesize findings from Steps 2–14, 16, and 17 into actionable outreach intel. **Do not run new web searches** — use only what was gathered in prior steps.
```

- [ ] **Step 12: Verify Step 15 circular reference fixed**

Run:
```bash
grep -n "Synthesize findings from Steps" company-research/SKILL.md
```
Expected: line now contains `Steps 2–14, 16, and 17`

- [ ] **Step 13: Verify Wave 2 read-scope current state**

Run:
```bash
grep -n "Read sanitized approved outputs from Steps 2" company-research/SKILL.md
```
Expected: one match — `│  Read sanitized approved outputs from Steps 2–9     │`

- [ ] **Step 14: Fix Wave 2 read-scope (Item 7)**

In `company-research/SKILL.md`, replace:
```
│    WAVE 2 — SPAWN AFTER SANITIZER COMPLETE          │
│  Workers: 10 (KServe Fit), 10B (ICP Score)          │
│  Read sanitized approved outputs from Steps 2–9     │
```
With:
```
│    WAVE 2 — SPAWN AFTER SANITIZER COMPLETE          │
│  Workers: 10 (KServe Fit), 10B (ICP Score)          │
│  Worker 10:  sanitized Steps 2–9                    │
│  Worker 10B: sanitized Steps 2–9, 11–14, 16–17      │
```

- [ ] **Step 15: Verify Wave 2 read-scope fixed**

Run:
```bash
grep -n "Worker 10B: sanitized Steps" company-research/SKILL.md
```
Expected: one match containing `Steps 2–9, 11–14, 16–17`

- [ ] **Step 16: Commit**

```bash
git add company-research/SKILL.md
git commit -m "fix(skill): structural and dependency corrections

Phase 7 items 2, 3, 4, 6, 7 — Step 1 explicit numbering, Step 6B
source table fallback column, Step 10B dependency to Steps 2-14,
Step 15 circular reference removed, Wave 2 read-scope split by worker."
```

---

## Task 3: Annotation / scope fixes (Items 5, 8, 9)

**Files:**
- Modify: `company-research/SKILL.md` — 3 edits in Checker Instructions, Orchestrator Instructions, and Sanitizer Instructions

- [ ] **Step 1: Verify Checker Criterion #7 current state**

Run:
```bash
grep -n "applies most strictly to Steps" company-research/SKILL.md
```
Expected: one match — `This criterion applies most strictly to Steps 8, 10, 12, 14, and 15.`

- [ ] **Step 2: Extend Checker Criterion #7 scope (Item 5)**

In `company-research/SKILL.md`, replace:
```
This criterion applies most strictly to Steps 8, 10, 12, 14, and 15.
```
With:
```
This criterion applies most strictly to Steps 8, 10, 12, 14, 15, 16, and 17.
```

- [ ] **Step 3: Verify Checker Criterion #7 updated**

Run:
```bash
grep -n "applies most strictly to Steps" company-research/SKILL.md
```
Expected: line now ends with `15, 16, and 17`

- [ ] **Step 4: Verify Orchestrator worker count current state**

Run:
```bash
grep -n "After all 19 Workers complete" company-research/SKILL.md
```
Expected: one match — `After all 19 Workers complete and each Checker has approved:`

- [ ] **Step 5: Annotate Orchestrator worker count (Item 8)**

In `company-research/SKILL.md`, replace:
```
After all 19 Workers complete and each Checker has approved:
```
With:
```
After all 19 Workers complete and each Checker has approved (19 = 17 Wave 1 Workers [Steps 2–9, 11–14, 16–17] + 2 Wave 2 Workers [Steps 10 + 10B]):
```

- [ ] **Step 6: Verify Orchestrator annotation added**

Run:
```bash
grep -n "19 = 17 Wave 1" company-research/SKILL.md
```
Expected: one match containing the full annotation

- [ ] **Step 7: Verify Sanitizer scope current state**

Run:
```bash
grep -n "What to scan" company-research/SKILL.md
```
Expected: one match — `**What to scan:** All approved Wave 1 outputs.`

- [ ] **Step 8: Add explicit step list to Sanitizer scope (Item 9)**

In `company-research/SKILL.md`, replace:
```
**What to scan:** All approved Wave 1 outputs. Note: Step 9's output is a synthesized artifact (scored summary of Step 8 data), not raw third-party content — the scan applies equally but may find lower injection surface.
```
With:
```
**What to scan:** All approved Wave 1 outputs (Steps 2–9, 11–14, 16–17 — 17 steps total). Note: Step 9's output is a synthesized artifact (scored summary of Step 8 data), not raw third-party content — the scan applies equally but may find lower injection surface.
```

- [ ] **Step 9: Verify Sanitizer scope updated**

Run:
```bash
grep -n "What to scan" company-research/SKILL.md
```
Expected: line now contains `Steps 2–9, 11–14, 16–17 — 17 steps total`

- [ ] **Step 10: Commit**

```bash
git add company-research/SKILL.md
git commit -m "fix(skill): annotation and scope corrections

Phase 7 items 5, 8, 9 — Checker criterion 7 now enforces Steps 16
and 17, Orchestrator worker count annotated with breakdown, Sanitizer
scope lists all 17 Wave 1 steps explicitly."
```

---

## Task 4: New content — Platform table + Tool absence protocol (Items 10 & 11)

**Files:**
- Modify: `company-research/SKILL.md` — 2 edits in Platform Execution Mode section and Core Research Principles

- [ ] **Step 1: Verify Platform table SEQUENTIAL row current state**

Run:
```bash
grep -n "SEQUENTIAL.*Single-thread" company-research/SKILL.md
```
Expected: one match ending with `Claude.ai · Cowork · Codex chat · Any single-thread assistant`

- [ ] **Step 2: Expand Platform Execution Mode SEQUENTIAL row (Item 10)**

In `company-research/SKILL.md`, replace:
```
| **SEQUENTIAL** | Single-thread only — one step at a time | Claude.ai · Cowork · Codex chat · Any single-thread assistant |
```
With:
```
| **SEQUENTIAL** | Single-thread only — one step at a time | Claude.ai · Claude Desktop (MCP) · Cowork · Codex chat · Cursor · VS Code Agent · Cline · Continue.dev · Windsurf · Any single-thread assistant |
```

- [ ] **Step 3: Verify SEQUENTIAL row updated**

Run:
```bash
grep -n "SEQUENTIAL.*Single-thread" company-research/SKILL.md
```
Expected: line now contains `Claude Desktop (MCP)` and `Cursor · VS Code Agent · Cline · Continue.dev · Windsurf`

- [ ] **Step 4: Verify graceful degradation paragraph location**

Run:
```bash
grep -n "Graceful degradation" company-research/SKILL.md
```
Expected: one match — `**Graceful degradation.** If a tool or data source is unavailable...`

- [ ] **Step 5: Add tool-absence protocol after Graceful degradation paragraph (Item 11)**

In `company-research/SKILL.md`, replace:
```
**Graceful degradation.** If a tool or data source is unavailable, note it clearly in that section and move on. Never halt the entire report because one step hit a wall.

**Rate-limited or gated sources.**
```
With:
```
**Graceful degradation.** If a tool or data source is unavailable, note it clearly in that section and move on. Never halt the entire report because one step hit a wall.

**Tool class unavailable.** If a required tool class is entirely absent from the executing environment — not rate-limited or gated, but simply not available — halt before starting and notify the user:

> ⚠️ Required tool missing: [web search / file write / subagents]. This skill cannot produce a reliable report without it. Please check your platform configuration or switch to a supported environment (see Platform Execution Mode table above).

Do not attempt to proceed in a partially capable environment. An incomplete report handed to BD is actively harmful.

**Rate-limited or gated sources.**
```

- [ ] **Step 6: Verify tool-absence protocol added**

Run:
```bash
grep -n "Tool class unavailable" company-research/SKILL.md
```
Expected: one match in Core Research Principles section

- [ ] **Step 7: Verify no unintended edits — spot-check key unchanged sections**

Run:
```bash
grep -n "Step 2 — Line of Business\|Step 8 — Reviews\|Step 15 — BD Intelligence\|Step 17 — Competitive" company-research/SKILL.md
```
Expected: all 4 headings present with their original titles

- [ ] **Step 8: Commit**

```bash
git add company-research/SKILL.md
git commit -m "fix(skill): platform table expansion and tool-absence protocol

Phase 7 items 10 & 11 — SEQUENTIAL platform list now includes Claude
Desktop (MCP), Cursor, VS Code Agent, Cline, Continue.dev, Windsurf;
new Core Research Principle halts on missing tool class before starting."
```

---

## Post-implementation: Mark Phase 7 complete in ROADMAP

- [ ] **Step 1: Mark all 12 Phase 7 items as shipped in ROADMAP.md**

In `ROADMAP.md`, for every `- [ ]` item under `## Phase 7 — Skill Standards & Quality`, change to `- [x]` and append `*(shipped: Phase 7 audit fixes — 2026-03-27)*`.

- [ ] **Step 2: Commit ROADMAP update**

```bash
git add ROADMAP.md
git commit -m "chore(roadmap): mark Phase 7 as complete

All 12 skill-creator audit items shipped in company-research/SKILL.md."
```
