# Execution status

This is the authoritative task-status record. The briefs and roadmap describe
planned work; they do not establish implementation progress.

Current state: task briefs prepared; implementation has not started.

| Task | State | Evidence report | Latest outcome or blocker |
| --- | --- | --- | --- |
| [01: ROM baseline](01-rom-baseline.md) | Not started | Pending | Earlier inspection supplied candidate filenames and hashes only. |
| [02: Source and symbols](02-source-and-symbols.md) | Not started | Pending | Requires task 01. |
| [03: Patch toolchain](03-patch-toolchain.md) | Not started | Pending | Requires tasks 01 and 02. |
| [04: Live battle state](04-live-battle-state.md) | Not started | Pending | Requires tasks 01-03. |
| [05: Damage routines](05-damage-routines.md) | Not started | Pending | Requires tasks 02-04. |
| [06: Single-move range](06-single-move-range.md) | Not started | Pending | Requires tasks 03-05. |
| [07: Isolation and regression](07-isolation-and-regression.md) | Not started | Pending | Requires tasks 04-06. |
| [08: Static menu display](08-static-menu-display.md) | Not started | Pending | Requires tasks 03-05. |
| [09: Live menu preview](09-live-menu-preview.md) | Not started | Pending | Requires tasks 06-08. |
| [10: Singles mechanics](10-singles-mechanics.md) | Not started | Pending | Requires task 09. |
| [11: Special mechanics](11-special-mechanics.md) | Not started | Pending | Requires task 10. |
| [12: Validation and release](12-validation-and-release.md) | Not started | Pending | Requires tasks 09-11. |

Allowed states: `Not started`, `In progress`, `Partial`, `Blocked`, `Complete`.
Keep task-specific details in the evidence report. When revising a completed
task or invalidating its assumptions, document the change and reassess dependent
tasks before treating their evidence as current.

Next task: [01 - Establish the ROM baseline](01-rom-baseline.md).
