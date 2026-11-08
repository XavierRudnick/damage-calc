# Radical Red in-game damage preview implementation plan

Status: planning only. No ROM, save, or implementation changes have been made.

## Objective

Display an accurate damage range for the highlighted attack inside Radical Red's
Fight menu. The final feature should run inside a patched GBA ROM, using the
game's damage mechanics. Use the existing TypeScript calculator as a comparison
tool during development.

This is a substantial ROM modification. An existing patch's author reports
displaying damage information in Radical Red 4.1's Fight menu, which supports
feasibility. Its implementation and compatibility need evaluation before reuse:
[author's release post](https://www.reddit.com/r/pokemonradicalred/comments/1txkarh/release_what_if_you_could_outsmart_the_ai/).

## Inspected baseline

Two different ROM builds were found in the local Downloads folder:

| File | Size | CRC32 | SHA-256 |
| --- | --- | --- | --- |
| `RadicalRed.gba` | 32 MiB | `FBA55DD8` | `679d112cdfe699c2793d82c7e7999ac9dfca9e222ad5a85d4f8f1e457cd0283f` |
| `1636 - Pokemon Fire Red (U)(Squirrels) (patched).gba` | 32 MiB | `A01196D1` | `a7f4b607fe1a04c29af95f02e82f8534c58d2b16d3df85044062957e8902ad82` |

Provisionally target `RadicalRed.gba`, which has associated saves. Confirm its
exact version before implementing any memory addresses or hooks. ROM headers and
filenames alone do not establish the Radical Red version.

Both files already occupy 32 MiB. Adding code requires identifying verified safe
space within the ROM and reserving appropriate RAM. Apparent unused bytes alone
are insufficient evidence that a region is safe to overwrite.

The workspace contains two independent component repositories:

- `damage-calc/`: TypeScript calculation engine and browser UI. The engine already
  includes Radical Red abilities such as Feline Prowess and Fatal Precision.
- `Rad-Red-4.1-Team-To-Calculator/`: mGBA Lua party exporter, Python watcher, and
  lookup tables. The exporter provides a starting point for memory inspection,
  but currently exports party information only. Accurate battle previews require
  the opponent and the full live battle state.

Matching game source, symbols, and a verified ROM address map have not been
established. Gameplay and preview behavior have not yet been tested.

## First version

Start with a damage preview for the highlighted move in single battles. Show it
in the move-details panel. The following numbers are illustrative:

```text
SURF
Damage: 72-85 HP
        36-43%
```

The percentage uses the target's maximum HP. Any eventual KO indicator compares
damage against its current HP and accounts for survival effects.

After the highlighted-move display works reliably, evaluate compact percentages
beside all four attacks.

## Architecture

```text
Live battle state
        |
        v
Isolated damage-range calculation
        |
        v
Highlighted move's details panel
```

Reuse verified game calculation routines where practical, preserving their
integer arithmetic, modifier order, and rounding. The TypeScript calculator
remains a development comparison tool; the native feature needs a GBA-compatible
implementation.

The preview calculation must not affect the actual battle. CFRU's AI damage
routine uses an approximate roll and modifies battle globals. Its damage code
also contains random-number calls. Audit the corresponding routines in the exact
target ROM before using them. A direct call to an AI damage estimate is not a
verified min/max calculation.

Reference:
[CFRU damage source](https://github.com/Skeli789/Complete-Fire-Red-Upgrade/blob/master/src/damage_calc.c).
This is reference code, not proof of the target ROM's exact implementation.

## Implementation phases

### 1. Establish the baseline

- Confirm the target ROM version and hash.
- Create separate working copies of the ROM and save.
- Establish a reproducible patch build.
- Make the patch process reject unsupported input ROMs.

Completion requirement: a documented, checksum-validated baseline and repeatable
build process.

### 2. Map the battle engine

- Seek matching source code or symbols first. Otherwise use mGBA's debugger and
  disassembly to establish the required addresses and calling conventions.
- Locate active battlers, stats, moves, abilities, items, stat stages, status,
  weather, terrain, screens, move cursor, and target selection.
- Locate the damage calculation path, random roll handling, and battle-menu
  rendering hooks.
- Verify every required address against observable battle changes. Do not assume
  ordinary FireRed offsets apply to Radical Red.

Completion requirement: a documented address map and battle snapshots that agree
with observable gameplay.

### 3. Prove accurate calculation

- Produce a range for one ordinary damaging move before adding the UI.
- Enumerate the target ROM's legal damage rolls, preserving calculation order
  and integer rounding.
- Isolate temporary calculation state and audit any reused routine's side
  effects. If a routine cannot be safely isolated, implement the required
  calculation in separate C code and verify it against the ROM.
- Confirm that previewing leaves RNG state, HP, items, abilities, battle flags,
  and other battle state unchanged.

Completion requirement: predicted damage matches actual controlled attacks, and
preview calls do not change battle outcomes.

### 4. Add the native display

- Hook the highlighted move's details rendering path.
- Allocate verified ROM and RAM space for code, text, and temporary data.
- Refresh when the selected move, target, or relevant battle state changes.
- Cache results where appropriate and invalidate them when their inputs change.
- Measure menu responsiveness and check for graphics corruption.

Completion requirement: a readable, stable preview throughout ordinary move
selection.

### 5. Expand mechanics coverage

- Add Radical Red abilities, held items, stat changes, status, weather, terrain,
  and screens.
- Cover forms, Mega Evolution, fixed damage, variable power, multi-hit attacks,
  survival effects, and double battles.
- Handle target selection and spread damage explicitly.
- Provide verified examples for each supported mechanic and show an explicit
  unknown result for unsupported cases.

Completion requirement: documented mechanics coverage with reproducible examples.

### 6. Validate and package

- Run calculation comparisons and gameplay regression checks.
- Check compatibility with mGBA and any other intended emulators or hardware.
- Package the source, build instructions, supported input hashes, and a
  checksum-validated BPS or UPS patch.
- Document save compatibility and known limitations based on actual testing.

Completion requirement: repeatable installation and documented compatibility.

## Accuracy rules

- Show ordinary damage conditional on the attack landing.
- Include guaranteed critical hits; handle random critical hits separately.
- Show status moves as `-` and confirmed immunities as `0`.
- Label moves whose damage depends on the opponent's action or another unresolved
  condition.
- Use actual battle stats and active effects, including transformations and
  changed abilities.
- Define multi-hit ranges explicitly, including possible hit counts.
- Treat percentages as damage relative to maximum HP, with KO evaluation based
  on current HP and survival effects.
- Assume a full-information calculator for the initial implementation. Reading
  the opponent's actual stats exposes information normally hidden from the
  player.

## Validation strategy

The ROM's actual attacks are the final reference. The browser calculator is a
useful second comparison; investigate any discrepancy rather than assuming
either implementation is correct.

Required checks:

- Controlled damage rolls match the displayed range.
- Repeated preview calculations leave battle state and RNG state unchanged.
- Identical battle inputs produce identical outcomes with the feature enabled
  and disabled.
- Switching, fainting, level-ups, Mega Evolution, target changes, and loading
  states continue to work.
- Menu navigation remains responsive without graphics corruption.

If calculator changes become necessary, add meaningful engine regressions under
`calc/src/test/` and run `npm test` from `damage-calc/`, as required by the
repository guidelines.

## Effort and first milestone

A useful native prototype is likely to take several weeks. Broad mechanics
coverage and compatibility could take months. These are preliminary planning
estimates; matching source or symbols could shorten the work substantially.
Reverse engineering the compiled ROM is the largest uncertainty.

The first implementation milestone is deliberately narrow:

**One highlighted move showing a verified damage range in a single battle, with
proof that previewing it cannot affect the battle.**

Use that milestone to establish whether the design is sound and refine the
remaining implementation estimate before expanding coverage.
