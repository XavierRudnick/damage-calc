# Task 03: build the patch toolchain

Milestone A. Suggested reasoning effort: High. Execute this task only.

## Read first

Read [WORKFLOW.md](WORKFLOW.md), [STATUS.md](STATUS.md), and the reports from
[task 01](01-rom-baseline.md) and [task 02](02-source-and-symbols.md):
`evidence/01-rom-baseline.md` and `evidence/02-source-and-symbols.md`.
Prerequisites: tasks 01 and 02 complete.

## Goal

Build a deterministic, hash-validated development pipeline that boots the target
with a copied save. Establish tools without introducing unverified native hooks.

## Work

1. Use task 02's selected route to inventory the required compiler, assembler,
   linker, debugger, and patch utilities. Check installed versions before adding
   dependencies. Record exact setup and build commands.
2. Keep the native component under `rom-preview/` and generated outputs under
   ignored `rom-preview/build/`. Add scoped ignore rules as needed. Avoid changing
   the browser build just to accommodate native tooling.
3. Implement build entry points that verify the selected input hash, preserve
   the source, and write outputs to a distinct path. Reject output paths that
   would overwrite the input ROM or original saves.
4. For a binary-patch route, begin with a deterministic baseline copy; this stage
   may be byte-identical to the input. For matching source, document how its
   baseline output corresponds to the target. A non-matching rebuild needs an
   explanation and investigation before later tasks rely on its addresses.
5. Prepare the native compilation scaffold using settings appropriate to the
   GBA CPU and the selected route. Keep hook addresses and memory allocation
   explicitly unresolved until verified in later tasks. Do not write into a
   padding region merely to demonstrate that code compiles.
6. Run the output in an isolated emulator instance with a working save copy.
   Record boot, title screen, save loading, and an ordinary gameplay check.
7. Document how to rebuild from a clean output directory and restore the local
   test environment. If emulator access is unavailable, record the missing check
   and leave completion pending.

## Artifacts

Provide build scripts, scoped native component scaffolding, and
`rom-preview/docs/build.md`. Store executable versions or dependency revisions
where reproducibility requires them. Do not track generated ROMs or states.

## Acceptance checks

- [ ] The input is validated and wrong hashes are rejected.
- [ ] Repeated builds from the same inputs produce identical output hashes.
- [ ] The original input and save are unchanged, and unsafe output paths fail.
- [ ] Build commands and dependencies are documented and reproducible.
- [ ] The generated baseline boots and loads the copied save successfully.
- [ ] No guessed ROM/RAM reservations or gameplay hooks were introduced.

## Handoff

Write `evidence/03-patch-toolchain.md` and update `STATUS.md`. Record the generated
ROM identity used for subsequent debugging. This completes milestone A when all
checks pass. The next task is [04 - Live battle state](04-live-battle-state.md).
