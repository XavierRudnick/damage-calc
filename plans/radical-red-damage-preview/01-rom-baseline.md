# Task 01: establish the ROM baseline

Milestone A. Suggested reasoning effort: High. Execute this task only.

## Read first

Read [WORKFLOW.md](WORKFLOW.md) and [STATUS.md](STATUS.md). There are no prerequisite
tasks. The [design overview](../../RADICAL_RED_IN_GAME_DAMAGE_PLAN.md) is background.

## Goal

Establish the exact local input ROM, preserve recoverable working copies, and
provide a repeatable way to verify identity before any patching occurs.

## Starting observations to recheck

The earlier read-only inspection found these files in the user's Downloads:

| Filename | Bytes | CRC32 | SHA-256 |
| --- | --- | --- | --- |
| `RadicalRed.gba` | 33554432 | `FBA55DD8` | `679d112cdfe699c2793d82c7e7999ac9dfca9e222ad5a85d4f8f1e457cd0283f` |
| `1636 - Pokemon Fire Red (U)(Squirrels) (patched).gba` | 33554432 | `A01196D1` | `a7f4b607fe1a04c29af95f02e82f8534c58d2b16d3df85044062957e8902ad82` |

There are associated `RadicalRed` saves and emulator states. The ROMs have a
FireRed header, which does not establish the Radical Red version. Provisionally
use `RadicalRed.gba`; do not substitute a different hash without documenting it.

## Work

1. Verify repository boundaries and inspect existing changes. Establish narrow
   ignore rules before creating local ROM/save copies under `rom-preview/local/`.
2. Recompute ROM size, CRC32, and SHA-256 with a repeatable verification tool.
   Record header metadata separately from claims about the hack's version.
3. Create a tracked target manifest containing filenames, hashes, source size,
   and version evidence. Avoid absolute local paths. An unconfirmed version must
   be recorded as unknown; exact hash identity can still support later research.
4. Inventory associated saves/states and record their sizes and local recovery
   locations. Preserve their bytes and names in untouched backup copies; do not
   assume their container formats from extensions or rewrite them.
5. Create separate experimental copies and document how to restore them. Ensure
   emulator experiments cannot overwrite the original save by sharing its path.
6. Make baseline verification fail clearly on the wrong input. Exercise failure
   using a temporary altered copy, without changing the original ROM.

## Scope and artifacts

Create baseline tooling under `rom-preview/tools/`, a manifest under
`rom-preview/target/`, and local-use instructions under `rom-preview/docs/`.
Modify ignore rules only as needed. Original ROMs and saves remain unchanged.
Do not install patch hooks, modify battle behavior, or start source analysis.

## Acceptance checks

- [ ] Selected ROM identity is reproducibly recorded and matches the manifest.
- [ ] Version evidence is recorded, or its absence is explicitly documented.
- [ ] Verification accepts the selected input and rejects an altered input.
- [ ] Original ROM/save hashes are unchanged after creating working copies.
- [ ] Recovery instructions identify the copied files and restoration steps.
- [ ] Git inspection confirms local ROMs, saves, states, and paths are excluded.

## Handoff

Write `evidence/01-rom-baseline.md` using the workflow's report format and update
`STATUS.md`. Include exact verification commands and the local artifact layout.
The next task is [02 - Source and symbols](02-source-and-symbols.md).
