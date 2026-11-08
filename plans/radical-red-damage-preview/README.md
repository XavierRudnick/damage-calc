# Radical Red damage preview: executable roadmap

Deliver a native GBA Fight-menu preview for the highlighted attack, showing a
verified damage range without changing the battle's behavior.

The [original design](../../RADICAL_RED_IN_GAME_DAMAGE_PLAN.md) supplies context.
The files below are the executable task briefs. This roadmap does not mean any
implementation has been completed; see [STATUS.md](STATUS.md) for current state.

## Give a task to a model

Use the following prompt, replacing the task filename:

```text
Read plans/radical-red-damage-preview/01-rom-baseline.md and execute that task
only. Follow its linked WORKFLOW.md, check STATUS.md and prerequisite evidence,
and preserve existing changes. Implement and validate the scoped deliverables.
Record verified findings, unresolved questions, and exact validation results in
the task's evidence report, then update STATUS.md. If a required prerequisite is
missing, document the specific gap and stop dependent work. Do not start the
next task automatically.
```

Run the model in this repository's working directory. For a new session, the task
file, workflow, status record, and prerequisite reports provide the handoff; the
previous chat is not required. Original ROMs and saves stay local.

## Task order

Recommended order is numerical. The dependencies below identify what must be
complete before a task can execute; independent work can be scheduled separately
when explicitly requested.

| Task | Brief | Prerequisites | Suggested effort |
| --- | --- | --- | --- |
| 01 | [Establish the ROM baseline](01-rom-baseline.md) | None | High |
| 02 | [Find matching source and symbols](02-source-and-symbols.md) | 01 | Extra High |
| 03 | [Build the patch toolchain](03-patch-toolchain.md) | 01, 02 | High |
| 04 | [Map live battle state](04-live-battle-state.md) | 01, 02, 03 | Extra High |
| 05 | [Trace damage and side effects](05-damage-routines.md) | 02, 03, 04 | Extra High |
| 06 | [Calculate one move's range](06-single-move-range.md) | 03, 04, 05 | Extra High |
| 07 | [Prove preview isolation](07-isolation-and-regression.md) | 04, 05, 06 | Extra High |
| 08 | [Render a static native menu preview](08-static-menu-display.md) | 03, 04, 05 | High |
| 09 | [Connect the highlighted move](09-live-menu-preview.md) | 06, 07, 08 | High |
| 10 | [Expand ordinary singles mechanics](10-singles-mechanics.md) | 09 | High; Extra High for discrepancies |
| 11 | [Expand special mechanics](11-special-mechanics.md) | 10 | Extra High |
| 12 | [Validate and package a release](12-validation-and-release.md) | 09, 10, 11 | High |

## Milestones

### A: establish feasibility, tasks 01-03

Produce a hash-locked baseline, source/reverse-engineering decision, and a
repeatable build that boots with a copied save. This is the first point at which
to revise implementation effort estimates using evidence.

### B: deliver the first working preview, tasks 04-09

Verify live data, damage calculation, and state isolation; add a native menu
display; then connect them. The milestone is complete when a supported ordinary
move has a verified range and browsing moves leaves battle outcomes unchanged.

### C: expand coverage and release, tasks 10-12

Add mechanics in independently verified batches, then package a reproducible
patch. Tasks 10 and 11 contain batch checkpoints and can take multiple sessions.
Publish supported and unsupported cases explicitly.

## Work organization

- Start with one implementing model. Suggested default: GPT-6.1 Sol at High
  effort, using Extra High for reverse engineering and calculation isolation.
- An independent reviewer is useful after tasks 05, 07, and 09. GPT-6 Astra is an
  optional choice for difficult reviews if available; model choice does not
  replace validation against the ROM.
- These settings carry forward the project's planning recommendations. Use
  settings supported by the current client; consult
  [OpenAI model guidance](https://learn.chatgpt.com/docs/models?surface=app) when
  choosing or updating them.
- Keep one active owner for ROM addresses, RAM reservations, and native hooks.
  Parallel work should have explicitly separate files and responsibilities.
- Detail the next task using prerequisite evidence. Later briefs deliberately
  avoid inventing ROM addresses, function signatures, or memory allocations.

## Planned file locations

All paths below are relative to the `damage-calc/` repository. The native paths
are proposed locations to create during implementation, not existing features.

| Path | Purpose |
| --- | --- |
| `rom-preview/` | Native patch component, kept separate from the browser engine |
| `rom-preview/tools/` | Baseline verification, build, inspection, and validation tools |
| `rom-preview/src/` | Native C and assembly, once addresses are verified |
| `rom-preview/target/` | Hash manifest, address map, layouts, and memory reservations |
| `rom-preview/tests/` | Native validation and sanitized fixtures |
| `rom-preview/docs/` | Build, calculation, coverage, and compatibility documentation |
| `rom-preview/local/` | Git-ignored ROM/save copies, states, and local captures |
| `rom-preview/build/` | Git-ignored generated binaries and build intermediates |
| `plans/radical-red-damage-preview/evidence/` | Per-task reports created as tasks execute |

If verified constraints require a different layout, document the reason and
update affected briefs before relying on the replacement paths. Follow
[WORKFLOW.md](WORKFLOW.md) for all tasks.
