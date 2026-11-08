# Task 07: prove preview isolation and add regression checks

Milestone B. Suggested reasoning effort: Extra High. Execute this task only.

## Read first

Read [WORKFLOW.md](WORKFLOW.md), [STATUS.md](STATUS.md), and reports
`evidence/04-live-battle-state.md`, `evidence/05-damage-routines.md`, and
`evidence/06-single-move-range.md` from tasks
[04](04-live-battle-state.md), [05](05-damage-routines.md), and
[06](06-single-move-range.md). Prerequisites: tasks 04-06 complete.

## Goal

Provide repeatable evidence that preview calls do not change actual battle
behavior, including all relevant RNG state and hidden bookkeeping.

## Work

1. Build on task 05's write inventory to define state invariants and narrowly
   owned scratch memory. Include globals, pointed-to data, RNG streams, item and
   ability flags, AI state, and execution state relevant to future battle behavior.
2. Capture before/after state at controlled execution points around one call and
   repeated calls. Distinguish the preview's allowed private scratch writes from
   changes to live battle state. Avoid comparisons across uncontrolled frames.
3. Run paired control/preview experiments from identical snapshots with identical
   input timing. Compare actual damage, criticals, secondary effects, AI actions,
   and subsequent turns where observable.
4. Exercise supported calculations, unavailable cases, repeated requests, and
   changing supported inputs. Check that fixture data and caller input snapshots
   remain unchanged by calculation.
5. Add deterministic damage regression fixtures and meaningful negative checks.
   Demonstrate that the isolation check detects a deliberate test-only state/RNG
   mutation and that a perturbed expected damage roll fails the comparison.
6. Document what is covered and what remains unproven. Correct state leakage
   within the assigned calculation/harness scope before declaring completion.

## Artifacts and scope

Deliver validation tooling and sanitized fixtures under `rom-preview/tests/` and
`rom-preview/tools/`, plus `rom-preview/docs/validation.md`. Explain how to run
local emulator-dependent checks and obtain needed local states. Do not replace
real ROM checks with a test that only repeats the preview implementation.

## Acceptance checks

- [ ] Damage fixtures pass against controlled target behavior.
- [ ] Single and repeated calls preserve audited battle state and RNG streams.
- [ ] Paired runs produce matching observable battle outcomes.
- [ ] Negative controls demonstrate that the checks detect relevant failures.
- [ ] Unavailable results and changed input snapshots are exercised.
- [ ] Emulator checks actually run; missing access is recorded as unfinished.

## Handoff

Write `evidence/07-isolation-and-regression.md` and update `STATUS.md`. Independent
review is recommended. Live integration cannot proceed until this gate passes.
Next in numerical order: [08 - Static menu display](08-static-menu-display.md).
