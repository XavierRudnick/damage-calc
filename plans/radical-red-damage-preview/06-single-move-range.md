# Task 06: calculate one move's exact damage range

Milestone B. Suggested reasoning effort: Extra High. Execute this task only.

## Read first

Read [WORKFLOW.md](WORKFLOW.md), [STATUS.md](STATUS.md), and reports
`evidence/03-patch-toolchain.md`, `evidence/04-live-battle-state.md`, and
`evidence/05-damage-routines.md` from tasks
[03](03-patch-toolchain.md), [04](04-live-battle-state.md), and
[05](05-damage-routines.md). Prerequisites: tasks 03-05 complete.

## Goal

Provide a GBA-compatible preview calculation for one controlled ordinary move,
matching the target ROM's damage rolls and integer rounding exactly.

## Work

1. Choose an available, reproducible single-hit damaging move and battle fixture
   whose relevant state is fully verified. State assumptions such as successful
   hit, ordinary critical state, current target, and supported modifiers.
2. Implement the route selected in task 05 under `rom-preview/src/`. Use verified
   inputs, calling conventions, and memory reservations. Native calculation must
   work independently of the browser and external services.
3. Define a small result contract: supported/unavailable state, reason when
   unavailable, minimum/maximum raw damage, and optional roll information for
   validation. Keep formatting separate from calculation.
4. Enumerate the target's legal damage rolls while preserving arithmetic order
   and rounding. Do not estimate the minimum by scaling a finished maximum unless
   the target's algorithm and validation prove that operation exact.
5. Compare every legal roll against real damage execution for the fixture using
   an isolated controlled runner or debugger. Keep test controls in local test
   copies; they must not become gameplay RNG manipulation in the feature.
6. Compare with the existing TypeScript calculator as a secondary check. Explain
   discrepancies using target evidence rather than adjusting to whichever result
   appears plausible. Unsupported cases must return unavailable.

## Artifacts and scope

Deliver the native implementation, the result contract, fixture expectations,
and reproduction instructions under `rom-preview/`. This task has no menu UI.
Initial state-preservation checks are required here; task 07 broadens them before
the implementation can be connected to live menu navigation.

## Acceptance checks

- [ ] The native component builds with the documented toolchain.
- [ ] Every legal roll for the selected fixture matches target execution.
- [ ] Minimum and maximum follow from verified rolls, with explicit assumptions.
- [ ] Missing inputs and unsupported cases return unavailable.
- [ ] Initial checks show no unintended battle-state or RNG changes.
- [ ] Reproduction does not require Chrome, Selenium, or the browser calculator.

## Handoff

Write `evidence/06-single-move-range.md` and update `STATUS.md`. Include fixture
identity, exact supported conditions, and roll comparison results. Next:
[07 - Isolation and regression](07-isolation-and-regression.md).
