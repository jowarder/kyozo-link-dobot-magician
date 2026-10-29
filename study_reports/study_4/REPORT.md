# Study 4

- **Rafiul Azim Jowarder**, Doctoral Student, Victor A. Zaloom Department of Industrial and Systems Engineering,
  Lamar University
- Supervisor: **Dr. James Curry**, Chair and Professor, Victor A. Zaloom Department of Industrial and Systems
  Engineering, Lamar University
- With help from **Wenhao Yang, Ph.D.**, Assistant Professor, Victor A. Zaloom Department of Industrial and Systems
  Engineering, Lamar University

## Real Dobot Magician

| Setting | Value |
|---|---|
| Dates | 2026-10-28 |
| Version | V4.5 (v3 — after Update 3), git commit `26ea23e` (v4.5-1-g26ea23e) |
| Session | 20 Tasks for Dobot (by itself) |
| Model | qwen3:4b-instruct-2507-q4_K_M, temperature 0.2, seed 42 |
| Cubes | 25.0 mm, set of 3 |
| Scoring | the watcher's camera look (V4.5 rules) |
| Tasks | Simple 20 (`Kyozo_Link/study/tasks/simple.yaml`), chained |
| Counting | One attempt per task; no collapse needed. |

### Results

| Measure | Value |
|---|---|
| Tasks | 20 |
| PASS | 13 |
| SOME PARTS (counted as FAIL) | 3 |
| FAIL | 4 |
| SKIPPED (counted as FAIL) | 0 |
| **Pass rate** | **13/20 (65%)** |
| Mean score (PASS=100, SOME=50, FAIL=0, SKIP=0) | 72.5 |
| Catastrophic tasks | 2 |
| Median position error (mm, tasks that ran) | 3.5 |
| Median angle error on turned cubes (deg) | 11.9 |

| Group | Pass rate |
|---|---|
| A: moves | 5/5 (100%) |
| B: swaps with a turn | 2/5 (40%) |
| C: towers of two | 4/5 (80%) |
| D: tower of three, drops | 2/5 (40%) |

Failures by type (SOME PARTS included): execution 5, plan 1, limit_alarm 1.

### Task by task

| Task | Group | Instruction | Outcome | Notes |
|---|---|---|---|---|
| S-01 | A | Move the red cube 40 mm further from the robot. | PASS | |
| S-02 | A | Move the blue cube 40 mm nearer the robot. | PASS | |
| S-03 | A | Move the green cube 50 mm further from the robot. | PASS | |
| S-04 | A | Move the green cube 50 mm nearer the robot. | PASS | |
| S-05 | A | Move the red cube 40 mm nearer the robot and the blue cube 40 mm further from the robot. | PASS | |
| S-06 | B | Swap the red and green cubes, then turn the red cube 45 degrees anticlockwise. | PASS | |
| S-07 | B | Swap the red and blue cubes, then turn the blue cube 30 degrees anticlockwise. | SOME PARTS | execution, 3.5 mm position error |
| S-08 | B | Swap the green and blue cubes, then turn the green cube 45 degrees clockwise. | SOME PARTS | execution, 4.4 mm |
| S-09 | B | Swap the blue and red cubes, then turn the red cube 30 degrees clockwise. | PASS | |
| S-10 | B | Swap the red and blue cubes, then turn both of them 30 degrees clockwise. | SOME PARTS | execution, 7.0 mm |
| S-11 | C | Put the red cube on the green cube. | PASS | |
| S-12 | C | Take the red cube off the green cube and put it to the right of the green cube with a 50 mm gap. | PASS | |
| S-13 | C | Put the blue cube on the green cube. | PASS | |
| S-14 | C | Take the tower apart: put the blue cube to the left of the green cube with a 45 mm gap. | FAIL · catastrophic | plan, 89.8 mm; blue cube ended outside the tray |
| S-15 | C | Put the green cube on the blue cube. | PASS | |
| S-16 | D | Take the green cube off the blue cube and put it to the right of the blue cube with a 40 mm gap. | FAIL · catastrophic | limit alarm; red cube moved 50 mm, green cube knocked off |
| S-17 | D | Build a tower with the green cube at the bottom, then the red cube, then the blue cube on top. | PASS | |
| S-18 | D | Take the blue cube off the tower and put it to the left of the tower with a 60 mm gap. | PASS | |
| S-19 | D | Take the red cube off the green cube, lift it 50 mm above the table to the right of the green cube with a 50 mm gap, and let it drop. | FAIL | execution, 25.1 mm |
| S-20 | D | Pick up the blue cube, lift it 40 mm above the table, move it 40 mm nearer the robot, and let it drop. | FAIL | execution, 23.4 mm |

### The angle-error drop

Study 3's angle error on turned cubes was 25.6°; Study 4's is 11.9°, a 2.3× reduction on the same six-cube sample.
This is the Update 3 change in action: the fingers angle check now accepts the measured ~20° gripper offset instead
of discarding it. Group B went from 0/5 pass in Study 3 to 2/5 pass in Study 4, with the three remaining Group B
failures all SOME PARTS (close on position, close on angle — the hardware's remaining scatter).

## What changed after Study 4

Narration v4: the update after Study 4 (V4.6, extending V4.5). Full account: `Kyozo_Link/study/NARRATION_v4.md`;
every change: `Kyozo_Link/study/CHANGES_v4.csv` (3 changes). V4.6 is in progress; no Study 5 yet.

Key changes:
- Each cube's turn is read from its coloured top face (reduces angle-reading noise on turned cubes).
- The last-released object must be seen in the next look (catches a cube that stayed stuck in the fingers after a
  release).
- A swap keeps each cube's level (what each stands on is noted first; each is put down where the other was at that
  level).
