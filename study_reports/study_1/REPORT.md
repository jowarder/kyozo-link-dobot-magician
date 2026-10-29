# Study 1

- **Rafiul Azim Jowarder**, Doctoral Student, Victor A. Zaloom Department of Industrial and Systems Engineering,
  Lamar University
- Supervisor: **Dr. James Curry**, Chair and Professor, Victor A. Zaloom Department of Industrial and Systems
  Engineering, Lamar University
- With help from **Wenhao Yang, Ph.D.**, Assistant Professor, Victor A. Zaloom Department of Industrial and Systems
  Engineering, Lamar University

## Real Dobot Magician

| Setting | Value |
|---|---|
| Dates | 2026-10-23 |
| Version | V4.1 (base), git commit `2f0030b` (v4.0-8-g2f0030b) |
| Session | 20 Tasks for Dobot (by itself) |
| Model | qwen3:4b-instruct-2507-q4_K_M, temperature 0.2, seed 42 |
| Cubes | 25 mm, set of 3 |
| Scoring | the watcher's camera look (re-scored under V4.5 rules) |
| Tasks | Simple 20 (`Kyozo_Link/study/tasks/simple.yaml`), chained: each starts where the last left the cubes |
| Counting | One outcome per task (best of attempts). See `../METHODOLOGY.md`. |

### Results

| Measure | Value |
|---|---|
| Tasks | 20 |
| PASS | 10 |
| SOME PARTS (counted as FAIL) | 0 |
| FAIL | 5 |
| SKIPPED (counted as FAIL) | 5 |
| **Pass rate** | **10/20 (50%)** |
| Mean score (PASS=100, SOME=50, FAIL=0, SKIP=0) | 50.0 |
| Catastrophic tasks | 0 |
| Median position error (mm, tasks that ran) | 3.3 |
| Median angle error on turned cubes (deg) | 27.6 |

| Group | Pass rate |
|---|---|
| A: moves | 4/5 (80%) |
| B: swaps with a turn | 1/5 (20%) |
| C: towers of two | 5/5 (100%) |
| D: tower of three, drops | 0/5 (0%) |

Failures by type on tasks that ran: execution 4, limit_alarm 1. Five Group D tasks were never attempted (SKIPPED) because of a camera-view bug in the watcher, fixed in V4.2.

### Task by task

| Task | Group | Instruction | Attempts, in order | Final outcome | Passed |
|---|---|---|---|---|---|
| S-01 | A | Move the red cube 40 mm further from the robot. | PASS | PASS | 1/1 |
| S-02 | A | Move the blue cube 40 mm nearer the robot. | PASS | PASS | 1/1 |
| S-03 | A | Move the green cube 50 mm further from the robot. | PASS | PASS | 1/1 |
| S-04 | A | Move the green cube 50 mm nearer the robot. | PASS | PASS | 1/1 |
| S-05 | A | Move the red cube 40 mm nearer the robot and the blue cube 40 mm further from the robot. | FAIL | FAIL | 0/1 |
| S-06 | B | Swap the red and green cubes, then turn the red cube 45 degrees anticlockwise. | SKIPPED, FAIL | FAIL | 0/2 |
| S-07 | B | Swap the red and blue cubes, then turn the blue cube 30 degrees anticlockwise. | SKIPPED, FAIL | FAIL | 0/2 |
| S-08 | B | Swap the green and blue cubes, then turn the green cube 45 degrees clockwise. | SKIPPED, FAIL | FAIL | 0/2 |
| S-09 | B | Swap the blue and red cubes, then turn the red cube 30 degrees clockwise. | SKIPPED, FAIL | FAIL | 0/2 |
| S-10 | B | Swap the red and blue cubes, then turn both of them 30 degrees clockwise. | SKIPPED, PASS | PASS | 1/2 |
| S-11 | C | Put the red cube on the green cube. | SKIPPED, PASS, PASS | PASS | 2/3 |
| S-12 | C | Take the red cube off the green cube and put it to the right of the green cube with a 50 mm gap. | SKIPPED, PASS, PASS | PASS | 2/3 |
| S-13 | C | Put the blue cube on the green cube. | SKIPPED, PASS, PASS | PASS | 2/3 |
| S-14 | C | Take the tower apart: put the blue cube to the left of the green cube with a 45 mm gap. | PASS | PASS | 1/1 |
| S-15 | C | Put the green cube on the blue cube. | PASS | PASS | 1/1 |
| S-16 | D | Take the green cube off the blue cube and put it to the right of the blue cube with a 40 mm gap. | SKIPPED | SKIPPED | 0/1 |
| S-17 | D | Build a tower with the green cube at the bottom, then the red cube, then the blue cube on top. | SKIPPED | SKIPPED | 0/1 |
| S-18 | D | Take the blue cube off the tower and put it to the left of the tower with a 60 mm gap. | SKIPPED | SKIPPED | 0/1 |
| S-19 | D | Take the red cube off the green cube, lift it 50 mm above the table to the right of the green cube with a 50 mm gap, and let it drop. | SKIPPED | SKIPPED | 0/1 |
| S-20 | D | Pick up the blue cube, lift it 40 mm above the table, move it 40 mm nearer the robot, and let it drop. | SKIPPED | SKIPPED | 0/1 |

### Failed and skipped attempts

- **S-05** `S-05_Run1` · FAIL · limit alarm: the arm couldn't reach the pose · position error 60.4 mm
- **S-06** to **S-13, S-16 to S-20** · the first attempts of these tasks were SKIPPED (the camera-view bug: the watcher could not see the table READY for the task). For S-06 to S-13 the next sitting ran the task; for S-16 to S-20 no retry was possible.
- **S-06** `S-06_Run2` · FAIL · execution · position error 70.3 mm
- **S-07** `S-07_Run2` · FAIL · execution · position error 1.0 mm (angle miss)
- **S-08** `S-08_Run2` · FAIL · execution · position error 2.8 mm (angle miss)
- **S-09** `S-09_Run2` · FAIL · execution · position error 114.4 mm

## Digital twin (simulation)

Same V4.1 code against the twin. Results from the engineer's package `For_Claude/study_1/20_Tasks_for_Twin/`.

| Measure | Value |
|---|---|
| Tasks | 20 |
| PASS | 4 (S-01 through S-04) |
| FAIL | 1 (S-05) |
| SKIPPED | 15 (the twin chain stopped after S-05's failure left the cubes where nothing could start) |
| **Pass rate** | **4/20 (20%)** |

## What changed after Study 1

Narration v1: the update after Study 1 (V4.3, extending V4.2). Full account: `Kyozo_Link/study/NARRATION_v1.md`;
every change: `Kyozo_Link/study/CHANGES_v1.csv` (12 changes). See `../../A1_version_diffs.md` for the grouped diff.

Key changes:
- The app looks at the table itself before the model's first turn (one turn fewer per request).
- The model may give every step it knows in one answer; `done()` tool added so the model does not spend a turn
  writing a summary.
- Wrist approach from one side folded into travel (one move fewer per pick and per place).
- Serial status reads reused for 2 s (6 fewer requests per move).
- Request checks and refusal messages sharpened (direction, held-object as destination, re-sent refusals).
- The per-task scene set-out was removed — tasks now start from the layout the previous task left behind. This is
  the change the paper credits with the Study 2 Dobot regression (see Study 2 report and paper Section VI-B).
- The watcher's output schema was extended (SOME PARTS, CATASTROPHIC, start condition) and this study's runs were
  re-scored under the new rules. The scorer change is the engineer's, logged in commit `40737df`.
