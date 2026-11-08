# Task 11: expand special mechanics

Milestone C. Suggested reasoning effort: Extra High. Execute this task only,
using separate checkpoints for each mechanics batch.

## Read first

Read [WORKFLOW.md](WORKFLOW.md), [STATUS.md](STATUS.md), and
`evidence/10-singles-mechanics.md` from [task 10](10-singles-mechanics.md).
Prerequisite: task 10 complete. Read the current mechanics coverage matrix and
its linked state, calculation, UI, and validation evidence.

## Goal

Extend verified coverage to special move behavior and battle configurations
without misrepresenting conditional or unresolved outcomes.

## Work in batches

1. **Create the special-case matrix.** Inventory target-specific special rules
   and required fixtures. Record which outcomes are determinable from current
   state and which depend on later choices, hit counts, or events. Set explicit
   batch checkpoints in the evidence report.
2. **Forms and transformations.** Verify Mega Evolution and applicable temporary
   stat/type/ability changes. Establish whether a preview is for the current
   form or a selected pending transformation and display that meaning clearly.
3. **Fixed and variable damage.** Cover applicable level-, HP-, speed-, weight-,
   and other state-based attacks using target arithmetic. Handle moves whose
   result depends on opponent actions with honest conditional/unavailable labels.
4. **Multiple hits and survival.** Define whether ranges are per hit or total,
   account for supported hit-count variation and per-hit changes, and verify
   relevant abilities. Account for Substitute, Sturdy, Focus Sash, False Swipe,
   and other applicable damage/survival limits according to the target. Distinguish
   raw damage from actual HP loss and any separately presented KO evaluation.
5. **Doubles and targeting.** Verify active slot/side mapping, chosen targets,
   spread modifiers, ally effects, and invalid/fainted targets. Show which target
   a result describes, especially before final target selection. Do not silently
   reuse singles assumptions.
6. **Regression and UI.** Add controlled fixtures and paired isolation checks for
   each new execution path. Exercise selecting/canceling transformations,
   switches, state loads, and target changes so stale results are detected.

## Artifacts and scope

Extend native code, target maps, fixtures, and
`rom-preview/docs/mechanics-coverage.md`. Update user-facing result semantics and
developer documentation where a single numeric range is insufficient. Maintain
per-batch progress in this task's report so work can span sessions.

If a case cannot be verified, provide a deliberate unavailable result and record
the exact gap. That preserves feature correctness but does not establish support
for that case. Do not claim full mechanics coverage while any cases remain open.

## Acceptance checks

- [ ] All listed batches have a documented support/limitation outcome.
- [ ] Implemented transformations and special damage paths match target fixtures.
- [ ] Multi-hit results identify their meaning and supported hit-count assumptions.
- [ ] Survival effects and KO semantics do not overstate actual outcomes.
- [ ] Doubles results identify the target and use verified targeting rules.
- [ ] Conditional/unsupported outcomes are explicit rather than misleading ranges.
- [ ] Isolation, refresh, and existing ordinary-singles regression checks pass.

## Handoff

Write and maintain `evidence/11-special-mechanics.md`, update `STATUS.md`, and
summarize exactly what a release can claim to support. Next:
[12 - Validation and release](12-validation-and-release.md).
