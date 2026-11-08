# Task 02: find matching source and symbols

Milestone A. Suggested reasoning effort: Extra High. Execute this task only.

## Read first

Read [WORKFLOW.md](WORKFLOW.md), [STATUS.md](STATUS.md), and the report produced by
[task 01](01-rom-baseline.md): `evidence/01-rom-baseline.md`.
Prerequisite: task 01 complete.

## Goal

Determine whether matching source or debug symbols exist for the selected ROM,
then establish an evidence-based development route.

## Work

1. Inspect task 01's manifest and version evidence. Identify any locally available
   source, linker maps, symbol files, patch metadata, or build instructions that
   could correspond to the selected hash.
2. Research primary project sources and relevant upstream engine code. Record
   repository URLs, exact revisions, build requirements, availability, and terms
   relevant to reusing code. Do not contact authors without user instructions.
3. Compare candidates against the ROM using concrete signatures, constants,
   disassembly, or reproducible output. Distinguish an exact match, a partially
   matching reference, and an unrelated implementation.
4. Evaluate any existing damage-preview patch as a reference if accessible.
   Record supported input hashes, source availability, and limitations. Keep the
   user's target unchanged; binary patch availability alone does not establish
   reusable source or compatibility.
5. Select the source-build route if evidence supports it. Otherwise document a
   bounded reverse-engineering route using the exact existing ROM, including
   which debugger/disassembler capabilities will be needed next.
6. List the unknowns to resolve in tasks 04 and 05, and revise effort assumptions
   based on evidence. Do not invent addresses to fill gaps in the assessment.

## Scope and artifacts

Produce `rom-preview/docs/source-assessment.md` and a source-reference manifest
under `rom-preview/target/` where useful. Keep downloaded source checkouts local
unless intentionally incorporating reviewed dependencies. This task makes no
battle-engine changes and does not migrate the project to a different game.

## Acceptance checks

- [ ] Source/symbol candidates have exact references and documented match quality.
- [ ] A source-build or reverse-engineering route is selected with reasons.
- [ ] Claims of correspondence include target-hash-specific evidence.
- [ ] Unavailable matching source is recorded honestly, without blocking this
      assessment's completion when a workable research route is established.
- [ ] Required tools, remaining unknowns, and build implications are documented.
- [ ] Original ROM and save remain unchanged.

## Handoff

Write `evidence/02-source-and-symbols.md` and update `STATUS.md`. A valid result
may be that matching source could not be established and reverse engineering is
required; document the search and limits of that conclusion. The next task is
[03 - Patch toolchain](03-patch-toolchain.md).
