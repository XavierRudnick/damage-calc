# Task 10: expand ordinary singles mechanics

Milestone C. Suggested reasoning effort: High; use Extra High when resolving
calculation discrepancies. Execute this task only, in the batches below.

## Read first

Read [WORKFLOW.md](WORKFLOW.md), [STATUS.md](STATUS.md), and
`evidence/09-live-menu-preview.md` from [task 09](09-live-menu-preview.md).
Prerequisite: task 09 complete. Follow the damage-path, state-map, and validation
references from that report before changing calculation behavior.

## Goal

Expand the proven prototype into an explicitly documented set of ordinary
single-battle calculations, retaining exact rounding and state isolation.

## Work in batches

1. **Define the coverage matrix.** Inventory relevant rules from the selected
   ROM and verified source. List supported inputs, required fixtures, expected
   behavior, and unavailable cases. Use the actual target's behavior rather than
   a generic generation's rules. Track a checkpoint after every batch so another
   session can resume without repeating completed research.
2. **Stats and basic modifiers.** Cover physical/special categories, stat stages,
   same-type bonuses, type effectiveness, relevant status effects, current/max
   HP dependence, and ordinary critical handling. Trace ordering and rounding.
3. **Field and sides.** Cover applicable weather, terrain, screens, and ordinary
   single-battle side effects. Extend verified state mapping and refresh inputs
   wherever the calculation needs additional data.
4. **Items and abilities.** Cover ordinary item/ability modifiers and suppression
   rules, including the Radical Red custom modifiers identified for this scope.
   Confirm each custom rule against target behavior. Do not assume the browser
   engine's implementation or ability labels exactly match the ROM.
5. **End-to-end regression.** For each batch, compare controlled roll outputs,
   run state-isolation checks, and verify the live UI after an affected input
   changes. Add interaction fixtures where modifier ordering can affect results.

## Artifacts and scope

Maintain `rom-preview/docs/mechanics-coverage.md` with fixture IDs and evidence
for every implemented rule family. Extend native code, verified maps, tests, and
cache invalidation as required. Update the checkpoint in this task's evidence
report after each batch. Do not fold browser rewrites into native coverage work.

Task 11 owns transformations, fixed/variable/multi-hit special execution,
survival effects, conditional moves, and doubles. Record those boundaries in the
matrix. Within ordinary singles, distinguish verified support from deferred or
unknown cases explicitly; do not label the whole game supported after checking
only a few moves.

## Acceptance checks

- [ ] Required rules in each ordinary-singles batch are enumerated and verified.
- [ ] Every implemented family has controlled target fixtures; interactions that
      can change ordering or rounding have additional cases.
- [ ] Relevant Radical Red custom modifiers have target-specific evidence.
- [ ] New inputs are mapped and refresh correctly in the live menu.
- [ ] Isolation checks pass for the expanded paths, including unavailable results.
- [ ] Coverage and remaining limitations are explicit, with no silent estimates.
- [ ] Any calculator-source changes pass its required `npm test` checks.

## Handoff

Write and maintain `evidence/10-singles-mechanics.md`, including batch progress
and coverage decisions, then update `STATUS.md`. Mark complete only after the
defined ordinary-singles batches pass their checks. Next:
[11 - Special mechanics](11-special-mechanics.md).
