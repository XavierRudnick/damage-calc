# Task 12: validate and package a release

Milestone C. Suggested reasoning effort: High. Execute this task only.

## Read first

Read [WORKFLOW.md](WORKFLOW.md), [STATUS.md](STATUS.md), and reports
`evidence/09-live-menu-preview.md`, `evidence/10-singles-mechanics.md`, and
`evidence/11-special-mechanics.md` from tasks
[09](09-live-menu-preview.md), [10](10-singles-mechanics.md), and
[11](11-special-mechanics.md). Prerequisites: tasks 09-11 complete. Consult the
baseline/build reports and current mechanics coverage before making release claims.

## Goal

Deliver a reproducible native patch with verified installation, compatibility,
regression evidence, and accurate support documentation.

## Work

1. Rebuild from documented inputs in a clean output location. Record source
   revision, tool versions, target input hash, and final output hash. Confirm
   deterministic output across repeated builds.
2. Run damage, isolation, formatting, and cache-invalidation checks across the
   supported coverage matrix. Investigate failures rather than removing checks
   or silently weakening supported behavior.
3. Run gameplay regression checks: move selection/cancel, target selection,
   switching, fainting, level-ups, evolution/Mega Evolution where supported,
   victory/loss transitions, saving/reloading, reset, and loading emulator states.
4. Establish the intended compatibility matrix. Actually test mGBA and each
   additional emulator/hardware target claimed as supported. Record versions,
   observations, performance, and untested environments distinctly. Do not
   generalize emulator results into hardware compatibility claims.
5. Generate a BPS or UPS patch against the exact supported base. Apply it to an
   untouched working copy and verify the output hash and boot behavior. Confirm
   wrong-base or corrupted inputs are rejected and an altered patch is detected.
6. Document installation, supported input hashes, result semantics, support
   limitations, save migration/recovery, build reproduction, and known issues.
   Test instructions from the intended user's starting point.
7. Prepare a local release package containing the patch, source/build references,
   and documentation. Inspect its contents and Git diff for local ROMs, saves,
   states, absolute machine paths, or unrelated edits. Publishing a GitHub release
   or distributing artifacts externally requires a user instruction to do so.

## Artifacts and scope

Produce release/build/compatibility documentation under `rom-preview/docs/` and
the local patch package in the ignored build output. Include patch checksums and
source revision in its manifest. Address defects within the preview feature; if
a defect requires a larger change to completed tasks, record and revalidate the
affected dependencies rather than disguising the change as packaging.

## Acceptance checks

- [ ] Repeated clean builds produce the documented output hash.
- [ ] Supported mechanics and isolation checks pass, with exact commands recorded.
- [ ] Gameplay regression and measured performance meet documented expectations.
- [ ] Every claimed compatibility target has actual test evidence.
- [ ] Patch application reproduces the output and rejects invalid inputs.
- [ ] Installation, limitations, save handling, and reproduction instructions work.
- [ ] Package/commit review confirms only intended source, patch metadata, and
      documentation are included; original game data stays local.

## Handoff

Write `evidence/12-validation-and-release.md` and update `STATUS.md`. Record the
local package path, source revision, exact checksums, and any remaining limitations.
Passing all acceptance checks completes milestone C for the documented scope.
Do not publish externally or start additional feature work automatically.
