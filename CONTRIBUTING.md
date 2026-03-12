# Contributing to KServe Skills

## Adding a new skill

1. Create a new directory: `<skill-name>/SKILL.md`
2. Add YAML frontmatter with `name` and `description`:
   ```yaml
   ---
   name: your-skill-name
   description: >
     [40+ words describing WHEN to use this skill, including example trigger phrases
     and what NOT to trigger on. The description is what the LLM uses for trigger matching
     — be specific about scope. E.g., "Use when the user asks to research a company for
     BD outreach. Do NOT trigger on general company questions that are not sales-related."]
   ---
   ```
3. Follow the **Worker → Checker → Orchestrator** pattern from `company-research` if the skill is multi-step:
   - Worker gathers data for one step
   - Checker validates against defined criteria (max 2 retries, then RETRY_EXHAUSTED)
   - Orchestrator assembles the final output
4. Include both **PARALLEL** and **SEQUENTIAL** execution modes if the skill has multiple steps
5. Provide an explicit **Output Format** template showing the exact structure the skill produces
6. Update `README.md`: add a row to the Available Skills table
7. Update `CHANGELOG.md` with the appropriate version bump (see Versioning section in README.md)
8. The npm `files` field (`"*/"` in package.json) auto-includes new skill directories — no package.json change needed

## Modifying an existing skill

| Change type | Version bump |
|---|---|
| Typo fix, instruction wording, Checker criteria clarification | Patch |
| New output field, new sub-section within an existing step, new Checker criterion | Minor |
| New step, workflow restructuring, breaking output format change | Minor (note "breaking output change" in CHANGELOG) |
| New skill added | Minor |

**Never modify a step instruction without testing it against at least 2 real company examples.** Run the skill on a known company (e.g., Zepto, PolicyBazaar, HDFC Ergo) and verify the output matches the intended change before merging.

## Code quality

- This is a pure Markdown/YAML repository — no build step, no linting
- All changes take effect immediately after merge
- Use the Worker → Checker → Orchestrator pattern for consistency across skills
- Every data point in output must have a source URL — this is a hard requirement enforced by the Checker
- Checkers must validate at minimum: source present, credible, recent, accurate, complete

## Step numbering

When adding steps to `company-research`:
- Sub-steps use letter suffixes: 6B, 7B, 7C, 10B (not 6.5 or 6a)
- New top-level steps require explicit dependency documentation in the Source Priority Reference table
- PARALLEL mode dependency changes must update the two-wave spawning instructions and the Orchestrator validation step

## Questions?

Open an issue on [GitHub](https://github.com/KServe-FMS/skills/issues).
