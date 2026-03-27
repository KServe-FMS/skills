# Design Spec: Company Research Skill — Enterprise ROADMAP

**Date:** 2026-03-27
**Skill:** `company-research`
**Current version:** v1.4.0
**Replaces:** `ROADMAP.md`

---

## Problem

The current `ROADMAP.md` has 46 items across 6 phases, with ~19 open. It covers the shipping backlog well but is not a full enterprise ambition document. It lacks:

- Global company research capability
- Many BD intelligence features needed for enterprise sales (BANT, deal sizing, personalized templates)
- Formal skill standards compliance tracking
- Depth in data quality, architecture resilience, and output delivery

The team needs a single enterprise master document that is comprehensive, prioritized, and structured to guide the skill from its current state to enterprise-grade.

---

## Goals

1. Replace `ROADMAP.md` with a comprehensive enterprise master document (100+ items)
2. Preserve all shipped history (`[x]` items) with their `*(shipped: ...)` notes
3. Expand all 6 existing phases with significantly more items
4. Add a 7th phase (Skill Standards & Quality) seeded from a skill-creator audit
5. Establish India as the primary research depth and global companies as a clearly-scoped secondary capability
6. Use a consistent item taxonomy with title, description, and BD/enterprise rationale

---

## Document Structure

```
ROADMAP.md
├── Header (purpose, current version, how to read)
├── Phase 1 — Research Coverage
│   ├── New Data Modules
│   ├── Depth Improvements to Existing Steps
│   ├── India-Primary Additions
│   └── Global Company Support (secondary capability)
├── Phase 2 — BD Intelligence
├── Phase 3 — Data Quality & Validation
├── Phase 4 — Workflow & Architecture
├── Phase 5 — Output & Delivery
├── Phase 6 — Platform & Integration
├── Phase 7 — Skill Standards & Quality (new)
└── Total item count
```

---

## Phase Expansion Plan

| Phase | Current items | Target items | Expansion direction |
|---|---|---|---|
| 1 — Research Coverage | 7 (6 shipped) | ~30 | India-specific registries, global adapters, new research modules |
| 2 — BD Intelligence | 8 (4 shipped) | ~25 | BANT, deal sizing, personalized templates, multi-stakeholder mapping |
| 3 — Data Quality | 7 (7 shipped) | ~15 | Confidence decay, cross-step contradiction matrix, staleness SLA |
| 4 — Workflow & Architecture | 8 (5 shipped) | ~20 | Batch, delta, watchlist, timeout handling, partial-run resume |
| 5 — Output & Delivery | 5 (0 shipped) | ~18 | JSON export, 1-pager, pitch brief, audit trail, multilingual |
| 6 — Platform & Integration | 3 (0 shipped) | ~12 | CRM creation, Slack/email, webhooks, API schema |
| 7 — Skill Standards & Quality | 0 | ~15 | Seeded from skill-creator audit findings |

**Total target: ~135 items**

---

## India-Primary / Global-Secondary Architecture

Phase 1 uses explicit sub-sections to separate India-depth from global capability. Global items do not break existing India-first behavior — they extend it.

```
### India-Primary Additions
Items that deepen India-specific research:
- GST registration & compliance
- EPFO filing signals
- CIBIL / credit bureau flags
- eCourts / NCLAT records
- Import/Export (Zauba / Volza)
- ROC / MCA deeper integration
- Tier-2/3 city intelligence
- Regional language review platforms

### Global Company Support (secondary capability)
Items that enable non-India company research:
- Global registry adapters (Companies House, SEC EDGAR, country equivalents)
- Multi-currency revenue normalization
- International review platforms
- Global job boards
- International regulatory risk signals
```

---

## Skill-Creator Integration

A formal skill-creator audit runs before the ROADMAP is written. Audit findings are incorporated as `- [ ]` items in Phase 7 with the audit finding quoted as rationale. The audit checks:

- YAML frontmatter and trigger description precision
- Step naming consistency and numbering integrity
- Checker criteria coverage and parity across steps
- PARALLEL/SEQUENTIAL behavioral equivalence
- Source table exhaustiveness and fallback completeness
- Output format template completeness
- Cross-reference accuracy (step numbers, wave assignments, orchestrator deps)

---

## Item Taxonomy

Every item follows this format:

```
- [ ] **Title** — one-sentence description of what it adds/fixes +
      one-sentence rationale (why it matters for enterprise BD)
      *(target phase: Phase X / depends on: Step Y)*  [optional, for complex deps]
```

Shipped items follow the existing convention:
```
- [x] **Title** — description *(shipped: Enhancement X.Y)*
```

---

## Execution Steps

1. Invoke `skill-creator` skill to audit `company-research/SKILL.md` against standards
2. Collect audit findings; map each to a Phase 7 item
3. Write expanded `ROADMAP.md` replacing current file — all 7 phases, ~135 items
4. Preserve all existing `[x]` shipped items verbatim
5. Commit the new `ROADMAP.md`

---

## Success Criteria

- ROADMAP.md has 7 phases with ~110–140 items total
- All existing shipped items are preserved
- India-primary and global-secondary are clearly separated within Phase 1
- Phase 7 contains at least 10 items from the skill-creator audit
- Every item has a description and rationale (no orphan titles)
- The document can stand alone as the definitive enterprise ambition doc for this skill
