# Task 04: map live battle state

Milestone B. Suggested reasoning effort: Extra High. Execute this task only.

## Read first

Read [WORKFLOW.md](WORKFLOW.md), [STATUS.md](STATUS.md), and the reports from
[01](01-rom-baseline.md), [02](02-source-and-symbols.md), and
[03](03-patch-toolchain.md): `evidence/01-rom-baseline.md`,
`evidence/02-source-and-symbols.md`, and `evidence/03-patch-toolchain.md`.
Prerequisites: tasks 01-03 complete.

## Goal

Obtain verified, coherent battle snapshots for the current attacker, defender,
selected move, and field. These snapshots will supply the preview calculation.

## Work

1. Use source correspondence or the debugger to locate active battle structures,
   battler IDs, party-to-battler mapping, and a reliable battle/menu-state signal.
   Treat existing Lua party offsets as candidates requiring independent checks.
2. Verify species/form, level, current/max HP, moves and PP, actual stats, stat
   stages, status, types, active ability, and held item for both active sides.
   Distinguish stored/base stats from already modified stats to prevent applying
   boosts or abilities twice.
3. Locate weather, terrain, screens, and other relevant field/side state. Map
   move cursor, current target, and selection lifecycle. Mark unverified or
   unavailable fields explicitly; do not substitute zero for unknown values.
4. Implement read-only diagnostic tooling under `rom-preview/tools/`. Validate
   any party decoding, encrypted layouts, or ability-slot interpretation against
   this ROM rather than assuming an ordinary FireRed or exporter layout.
5. Capture coherent snapshots at an identified stable point. Verify values
   against observations and controlled changes: changing move selection, losing
   HP, changing a stat stage, switching, and activating a field effect.
6. Handle leaving battle, invalid battler slots, reset, and loading a state.
   Stale or inconsistent data must be detectable instead of producing a preview.

## Artifacts and scope

Produce `rom-preview/target/battle-state-map.md` with addresses, sizes, layouts,
hash identity, and evidence. Define a documented snapshot schema and sanitized
fixtures under `rom-preview/tests/`. Keep raw captures/states local. This task
reads state; it does not execute damage routines or modify the game menu.

## Acceptance checks

- [ ] Both active sides and selected move/target are identified correctly.
- [ ] Values agree with controlled observations across the listed state changes.
- [ ] Every mapped field records verification evidence; unknown fields stay
      unknown and limit what later calculations can claim to support.
- [ ] Snapshot capture is coherent and does not modify battle memory.
- [ ] Leaving battle, switching, reset, and state loading invalidate stale data.
- [ ] Diagnostic steps and fixture reproduction are documented.

## Handoff

Write `evidence/04-live-battle-state.md` and update `STATUS.md`. Record which
snapshot fields are sufficient for a first ordinary-move fixture and which
mechanics remain unavailable. Next: [05 - Damage routines](05-damage-routines.md).
