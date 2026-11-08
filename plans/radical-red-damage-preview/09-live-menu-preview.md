# Task 09: connect the highlighted move to a live preview

Milestone B. Suggested reasoning effort: High. Execute this task only.

## Read first

Read [WORKFLOW.md](WORKFLOW.md), [STATUS.md](STATUS.md), and reports
`evidence/06-single-move-range.md`, `evidence/07-isolation-and-regression.md`, and
`evidence/08-static-menu-display.md` from tasks
[06](06-single-move-range.md), [07](07-isolation-and-regression.md), and
[08](08-static-menu-display.md). Prerequisites: tasks 06-08 complete. Also consult
the battle-state and memory maps referenced by those reports.

## Goal

Show verified damage for a supported highlighted move in a single battle, with
correct refresh and unchanged gameplay. This is the first useful native feature.

## Work

1. Replace task 08's placeholder with task 06's calculation result using task 04's
   coherent current-state snapshot. Execute at a verified safe lifecycle point.
2. Format raw HP and percentages of target maximum HP using documented integer
   rounding. Allow values over 100 percent when appropriate. Use current HP only
   for any separately supported KO evaluation.
3. Represent unavailable cases explicitly. Status, immunity, fixed damage, and
   conditional moves may receive specific labels only when classified correctly;
   avoid displaying a verified numerical range for unsupported mechanics.
4. Refresh on move, attacker, defender, HP, stats, stages, status, item, ability,
   form, and relevant field changes. If caching is used, key it by all inputs the
   supported calculation actually uses. Clear it on reset, battle transitions,
   switching, and state loads.
5. Keep expensive work out of repeated rendering when possible. Measure the
   actual latency and emulator performance; select an acceptable budget using
   observations and document it.
6. Repeat task 07's paired outcomes with the UI enabled/disabled and identical
   inputs. Verify changing cursor positions does not introduce extra RNG or AI
   work. Exercise repeated menu use and the selected-move/target lifecycle.

## Artifacts and scope

Deliver the integrated native preview, formatting and refresh checks, and updated
validation/UI documentation under `rom-preview/`. Stay within verified ordinary
single-battle support. Preserve explicit unavailable behavior for the remainder;
tasks 10 and 11 own wider coverage.

## Acceptance checks

- [ ] A supported highlighted move displays the exact verified HP range.
- [ ] Percentages use maximum HP with documented rounding and no misleading cap.
- [ ] Relevant state changes refresh the result without stale values.
- [ ] Unsupported or invalid state never produces a plausible-looking estimate.
- [ ] UI-enabled/disabled paired runs preserve battle outcomes and audited state.
- [ ] The native feature works without browser processes and remains responsive.

## Handoff

Write `evidence/09-live-menu-preview.md` and update `STATUS.md`. Include a
reproducible demonstration and exact supported conditions. Independent review is
recommended. Passing this task completes milestone B. Next:
[10 - Singles mechanics](10-singles-mechanics.md).
