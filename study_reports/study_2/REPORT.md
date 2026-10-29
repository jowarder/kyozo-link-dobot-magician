# Study 2

- **Rafiul Azim Jowarder**, Doctoral Student, Victor A. Zaloom Department of Industrial and Systems Engineering,
  Lamar University
- Supervisor: **Dr. James Curry**, Chair and Professor, Victor A. Zaloom Department of Industrial and Systems
  Engineering, Lamar University
- With help from **Wenhao Yang, Ph.D.**, Assistant Professor, Victor A. Zaloom Department of Industrial and Systems
  Engineering, Lamar University

## Real Dobot Magician

Study 2 had **two sittings** on 2026-10-26. The first sitting (`2026-10-26_123244`, 12:32) was stopped by hardware
faults — a lost USB link, then a controller stuck in alarm `0x12` after S-05. The second sitting (`2026-10-26_180835`,
18:08) ran the full chain. **Per the pre-registration (`Kyozo_Link/study/PREREG.md`), an interrupted sitting is retried
and only the complete sitting is reported.** This report counts the second sitting only.

| Setting | Value |
|---|---|
| Dates | 2026-10-26 (second sitting, 18:08) |
| Version | V4.3 (v1 — after Update 1), git commit `f07c20e` (v4.2-2-gf07c20e) |
| Session | 20 Tasks for Dobot (by itself) |
| Model | qwen3:4b-instruct-2507-q4_K_M, temperature 0.2, seed 42 |
| Cubes | 25 mm, set of 3 |
| Scoring | the watcher's camera look (re-scored under V4.5 rules) |
| Tasks | Simple 20 (`Kyozo_Link/study/tasks/simple.yaml`), chained |
| Counting | One outcome per task from the second sitting. See `../METHODOLOGY.md`. |

### Results

| Measure | Value |
|---|---|
| Tasks | 20 |
| PASS | 4 |
| SOME PARTS (counted as FAIL) | 0 |
| FAIL | 16 |
| SKIPPED (counted as FAIL) | 0 |
| **Pass rate** | **4/20 (20%)** |
| Mean score (PASS=100, SOME=50, FAIL=0, SKIP=0) | 20.0 |
| Catastrophic tasks | 5 |
| Median position error (mm, tasks that ran) | 40.1 |
| Median angle error on turned cubes (deg) | 30.3 |

| Group | Pass rate |
|---|---|
| A: moves | 4/5 (80%) |
| B: swaps with a turn | 0/5 (0%) |
| C: towers of two | 0/5 (0%) |
| D: tower of three, drops | 0/5 (0%) |

Failures by type: plan 7, execution 7, preparation 2.

### Task by task (second sitting)

| Task | Group | Instruction | Outcome | Notes |
|---|---|---|---|---|
| S-01 | A | Move the red cube 40 mm further from the robot. | PASS | |
| S-02 | A | Move the blue cube 40 mm nearer the robot. | PASS | |
| S-03 | A | Move the green cube 50 mm further from the robot. | FAIL | execution, 16.5 mm position error |
| S-04 | A | Move the green cube 50 mm nearer the robot. | PASS | |
| S-05 | A | Move the red cube 40 mm nearer the robot and the blue cube 40 mm further from the robot. | PASS | |
| S-06 | B | Swap the red and green cubes, then turn the red cube 45 degrees anticlockwise. | FAIL | plan, 116.8 mm |
| S-07 | B | Swap the red and blue cubes, then turn the blue cube 30 degrees anticlockwise. | FAIL · catastrophic | execution, 180.5 mm; blue cube ended outside the tray |
| S-08 | B | Swap the green and blue cubes, then turn the green cube 45 degrees clockwise. | FAIL | plan, 120.7 mm |
| S-09 | B | Swap the blue and red cubes, then turn the red cube 30 degrees clockwise. | FAIL · catastrophic | execution, 203.6 mm; cubes ended outside the tray |
| S-10 | B | Swap the red and blue cubes, then turn both of them 30 degrees clockwise. | FAIL | plan, 85.1 mm |
| S-11 | C | Put the red cube on the green cube. | FAIL · catastrophic | plan; red cube knocked off the table |
| S-12 | C | Take the red cube off the green cube and put it to the right of the green cube with a 50 mm gap. | FAIL · catastrophic | preparation; red cube knocked off the table |
| S-13 | C | Put the blue cube on the green cube. | FAIL | plan, 25.9 mm |
| S-14 | C | Take the tower apart: put the blue cube to the left of the green cube with a 45 mm gap. | FAIL | execution, 81.3 mm |
| S-15 | C | Put the green cube on the blue cube. | FAIL | plan, 26.7 mm |
| S-16 | D | Take the green cube off the blue cube and put it to the right of the blue cube with a 40 mm gap. | FAIL | execution, 77.8 mm |
| S-17 | D | Build a tower with the green cube at the bottom, then the red cube, then the blue cube on top. | FAIL | plan, 26.2 mm |
| S-18 | D | Take the blue cube off the tower and put it to the left of the tower with a 60 mm gap. | FAIL | execution, 96.3 mm |
| S-19 | D | Take the red cube off the green cube, lift it 50 mm above the table to the right of the green cube with a 50 mm gap, and let it drop. | FAIL · catastrophic | preparation; red cube knocked off the table |
| S-20 | D | Pick up the blue cube, lift it 40 mm above the table, move it 40 mm nearer the robot, and let it drop. | FAIL | plan, 40.1 mm |

### Why the regression

Update 1 removed the per-task scene set-out (V4.1 reorganised the cubes to a known layout before each task; V4.3 let
each task begin from the layout the previous task left behind, to save model turns and wall time). On the arm this
meant tasks starting from cube positions near the reach boundary or close enough together to confuse the detector,
which the model could not always plan around. The twin missed it because the twin's cubes always began in reachable,
well-separated positions regardless of what came before — the twin passed 19 of 20 before this release.

## Digital twin (simulation)

| Measure | Value |
|---|---|
| Tasks | 20 |
| PASS | 19 (every task but S-16) |
| FAIL | 1 (S-16) |
| **Pass rate** | **19/20 (95%)** |

Pre-release gate the day before Study 2. The gap of 75 points (twin 95%, arm 20%) is the "twin forecast gap" the
paper reports in its results table; it was the signal that the loop had introduced a sim-to-real gap, and Update 2
closed most of it.

## What changed after Study 2

Narration v2: the update after Study 2 (V4.4, extending V4.3). Full account: `Kyozo_Link/study/NARRATION_v2.md`;
every change: `Kyozo_Link/study/CHANGES_v2.csv` (15 changes). See `../../A1_version_diffs.md` for the grouped diff.

Key changes:
- `RobotNeedsPerson`: the arm halts and waits for a person after a connect without Home, a lost USB link, or an alarm
  the controller cannot clear. Addressed the catastrophic events.
- Controller joint-limit model fitted to 323 real moves from Study 2; every target checked before it is sent.
- Two touching cubes split into two tops (flat top with two colour groups).
- Narrow-side cube measurements kept so a cube is not confused with another cube size.
- Watcher status strip clarified; no scoring-rule change.

## About the aborted first sitting

The first sitting (12:32) completed S-01 through S-05 on the arm (some failed on hardware, same V4.3 code), then the
watcher could not start S-06 to S-13 because the detector could not see the table ready for a swap/tower task after
the preceding failure left cubes near the base. The engineer stopped the sitting when the controller got stuck in a
0x12 limit alarm and refused every move. The arm was power-cycled, re-homed, and the full chain was re-run that
evening. The first sitting's raw data is preserved under `Kyozo_Link_Results/study_2/20_Tasks_for_Dobot/_raw_data/`
but is not counted in the headline numbers above, per the pre-registration.
