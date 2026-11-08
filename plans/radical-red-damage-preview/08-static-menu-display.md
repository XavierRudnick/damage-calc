# Task 08: render a static native menu preview

Milestone B. Suggested reasoning effort: High. Execute this task only.

## Read first

Read [WORKFLOW.md](WORKFLOW.md), [STATUS.md](STATUS.md), and reports
`evidence/03-patch-toolchain.md`, `evidence/04-live-battle-state.md`, and
`evidence/05-damage-routines.md` from tasks
[03](03-patch-toolchain.md), [04](04-live-battle-state.md), and
[05](05-damage-routines.md). Prerequisites: tasks 03-05 complete. This task may
be scheduled independently of 06-07 when explicitly requested; it uses static
text and never invokes the preview calculation.

## Goal

Establish a stable native Fight-menu rendering hook and usable layout before
connecting live damage calculation.

## Work

1. Trace menu entry, cursor changes, details rendering, target selection, and
   exit. Identify the correct rendering lifecycle and original code to preserve.
2. Verify hook boundaries, displaced instructions, register/stack conventions,
   branch reach, text encoding, window/tile ownership, and cleanup behavior.
3. Establish documented, non-overlapping ROM/RAM reservations with evidence.
   Check references and runtime ownership rather than relying on padding bytes.
   Keep all changes within the target ROM's supported address space and size.
4. Add a native display of clearly marked development placeholder values in the
   highlighted move's details area. Keep move names, PP, type, and menu controls
   readable. The final layout must suit the GBA's actual screen dimensions.
5. Check all four cursor positions, entering/leaving Fight, canceling selection,
   returning after attacks, switching, and menu reconstruction after state load.
6. Build reproducibly and visually inspect the output in the isolated emulator.
   Measure responsiveness and record local screenshots and observations.

## Artifacts and scope

Deliver native UI/hook code under `rom-preview/src/`, a memory reservation map
under `rom-preview/target/`, and UI notes under `rom-preview/docs/`. Keep a visual
test record; screenshots are local by default. This task adds static text only.
It must not invoke damage or AI routines or change move-selection behavior.

## Acceptance checks

- [ ] Hook addresses, conventions, and allocated memory have recorded evidence.
- [ ] Placeholder text renders legibly without overlapping essential information.
- [ ] Cursor movement and menu entry/exit behave normally.
- [ ] Repeated redraws, switching, and state loading do not corrupt graphics.
- [ ] No damage calculation or AI execution was added to the rendering path.
- [ ] Visual checks and build reproduction steps are recorded.

## Handoff

Write `evidence/08-static-menu-display.md` and update `STATUS.md`. Next:
[09 - Live menu preview](09-live-menu-preview.md), after tasks 06 and 07 also pass.
