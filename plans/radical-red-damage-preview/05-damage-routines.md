# Task 05: trace damage calculation and side effects

Milestone B. Suggested reasoning effort: Extra High. Execute this task only.

## Read first

Read [WORKFLOW.md](WORKFLOW.md), [STATUS.md](STATUS.md), and prerequisite reports
`evidence/02-source-and-symbols.md`, `evidence/03-patch-toolchain.md`, and
`evidence/04-live-battle-state.md` from tasks
[02](02-source-and-symbols.md), [03](03-patch-toolchain.md), and
[04](04-live-battle-state.md). Prerequisites: tasks 02-04 complete.

## Goal

Explain how the target ROM calculates damage and establish a viable, isolated
path for computing a range. Produce evidence before calling routines for a UI.

## Work

1. Trace actual execution for an ordinary physical and special attack. Identify
   base damage, type/ability/item/field modifiers, random roll application,
   critical-hit handling, minimum damage, and integer rounding order.
2. Identify candidate callable routines and document inputs, outputs, calling
   conventions, required global context, and transitive dependencies. Distinguish
   file offsets from CPU addresses and ARM/Thumb entry conventions.
3. Audit writes and nonlocal effects: battle globals, pointed-to structures,
   item/ability recording, AI caches, random generators, callbacks, and scripts.
   Record all discovered RNG streams, not just a conventional FireRed seed.
4. Compare real move execution with AI damage estimates. Determine what each
   routine omits or approximates and why an AI estimate may not supply exact
   min/max damage. Verify the target's legal rolls instead of assuming them.
5. Select an implementation route for task 06: safely reusable native routines,
   isolated native C reproducing verified logic, or an explicitly justified
   combination. Explain how it avoids observed side effects and what remains
   to be demonstrated by tests.
6. Identify candidate hook and scratch-space requirements for later work, with
   verification evidence. Leave unknown addresses unresolved; this task is not
   authorization to overwrite apparently unused ROM/RAM.

## Artifacts and scope

Produce `rom-preview/docs/damage-path.md` and a target-specific routine map under
`rom-preview/target/`. Record short supporting traces and findings, keeping raw
dumps local. Include the selected route, an input/output contract, and a side
effect inventory. Do not install a per-frame preview call or a menu hook.

## Acceptance checks

- [ ] Real damage execution is traced for ordinary physical and special moves.
- [ ] Random rolls, rounding, and critical handling have target-specific evidence.
- [ ] Candidate routines have documented interfaces and side-effect inventories.
- [ ] Approximate AI behavior is distinguished from actual damage execution.
- [ ] A credible route for task 06 is documented, including remaining uncertainty.
- [ ] Findings are sufficient for an independent reviewer to challenge the route.

## Handoff

Write `evidence/05-damage-routines.md` and update `STATUS.md`. An independent
review is recommended before implementing native calls. Next:
[06 - Single-move range](06-single-move-range.md).
