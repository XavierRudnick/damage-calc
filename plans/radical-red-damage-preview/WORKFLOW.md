# Shared execution and handoff instructions

These instructions apply to every task in this directory. Read the assigned
brief and [STATUS.md](STATUS.md) before implementing it.

## Start each task

1. Read the workspace and component `AGENTS.md` instructions. Run Git commands
   inside the component being changed; verify its top-level path and remote.
2. Inspect existing changes. Preserve unrelated edits and generated team files.
   Never discard or include them in the task's commit.
3. Read the prerequisite task reports linked by the brief. Confirm the relevant
   acceptance checks passed, and that their target ROM hash still matches.
4. If a prerequisite is missing, perform useful work that does not depend on it,
   record the exact gap, and leave dependent work incomplete. Do not execute a
   different task silently or invent missing evidence.
5. Set the assigned row in `STATUS.md` to `In progress`. Work on this task only.
   Do not launch parallel agents unless the user explicitly requests them.

## Scope and repository boundaries

- The native component belongs under `damage-calc/rom-preview/`; create it as
  needed. The browser calculator remains the comparison tool.
- Keep native tooling independent of the browser build and its dependencies
  unless an actual integration need is demonstrated.
- Treat the sibling `Rad-Red-4.1-Team-To-Calculator/` repository as a read-only
  reference unless the assigned task and user authorize a specific change.
  Its party offsets and ability/EV reconstruction require independent validation.
- A task may update its own brief, its evidence report, `STATUS.md`, and directly
  relevant native files. Record justified changes to shared interfaces.
- Preserve original ROMs, saves, states, and the current emulator session. Run
  experiments against working copies. Use a separate emulator process where
  needed; avoid saving experimental state over the user's live game.
- Before copying ROMs or saves into the repository, establish narrow ignore
  rules for `rom-preview/local/` and `rom-preview/build/`. Keep ROM/save images,
  emulator states, raw memory dumps, and machine-specific configuration out of
  commits. Review screenshots or fixtures before tracking them.
- Record target hashes and filenames in tracked manifests. Resolve local paths
  through arguments or ignored local configuration.
- Do not automatically commit or push implementation work. Do so when requested
  for that task; include only the assigned task's files.

## Evidence and calculation rules

- The inspected provisional target is `RadicalRed.gba`, 33,554,432 bytes, CRC32
  `FBA55DD8`, SHA-256
  `679d112cdfe699c2793d82c7e7999ac9dfca9e222ad5a85d4f8f1e457cd0283f`.
  Recompute identity in task 01. Version, addresses, and calling conventions
  remain unverified until supported by recorded evidence.
- Distinguish verified facts, candidate interpretations, and unknowns. Associate
  addresses and layouts with the exact target hash and supporting observations.
- Upstream FireRed/CFRU source, existing exporter offsets, community patches,
  and the browser calculator are references. Establish correspondence to this
  ROM before treating any of them as authoritative for its behavior.
- Both inspected ROMs occupy 32 MiB. A run of padding bytes does not establish
  that a ROM region is free; RAM and hook locations also require evidence.
- Preserve integer arithmetic, modifier order, and rounding. Determine actual
  legal damage rolls and critical-hit rules from the target implementation.
- Audit side effects, including all RNG streams, globals, caches, callbacks,
  item/ability bookkeeping, and pointed-to structures. Restoring one RNG seed
  is insufficient evidence of isolation.
- The preview describes damage conditional on landing against the current
  target in the current state. Percentages use maximum HP. KO evaluation uses
  current HP and survival effects. Conditional mechanics need explicit labels.
- Initially assume full-information access to the opponent. The native feature
  must operate without the browser, Selenium, or an external calculator service.
- Unknown or unsupported calculations must yield an explicit unavailable result.
  Never substitute a plausible numerical estimate and label it verified.

## Validation

Run checks appropriate to the task and record exact commands and outcomes.
Separate static inspection, automated tests, emulator observations, and unrun
checks. Mark missing emulator access or required battle fixtures explicitly.

If calculator source changes are necessary, follow repository guidelines: engine
regressions belong in `calc/src/test/`, and run `npm test` from `damage-calc/`.
UI source changes require the normal build and visible checks. Native-only work
needs its own documented build and ROM validation rather than assuming the
calculator's tests exercise it.

## Complete the handoff

Create `evidence/NN-task-name.md` using the filename specified by the task. Include:

1. Task ID, execution date, target ROM hash, and relevant source revision.
2. Outcome: complete, partial, or blocked, with acceptance-check results.
3. Changed files and how to reproduce the work.
4. Verified findings and the commands, traces, or observations supporting them.
5. Candidate interpretations and unresolved questions, clearly separated.
6. Validation commands, outputs or concise summaries, and checks not run.
7. Local-only artifact locations using workspace-relative paths where practical.
8. Known risks, unsupported cases, and the exact next task or missing input.

Update `STATUS.md` with the report link and a short factual outcome. Mark a task
`Complete` only when all its acceptance checks have passed. Use `Partial` for
unfinished work and `Blocked` when a specific prerequisite or external input
prevents dependent work; this document's labels describe tasks, not any separate
goal-management tool status.

When no implementation task has executed, leave it `Not started`. Planning and
creating these briefs do not complete their acceptance checks. Finish with a
concise user-facing handoff and do not start the next task automatically.
