# Study 3

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
| Version | V4.4 (v2 — after Update 2), git commit `175dfed` (v4.3-14-g175dfed) |
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
| PASS | 12 |
| SOME PARTS (counted as FAIL) | 3 |
| FAIL | 5 |
| SKIPPED (counted as FAIL) | 0 |
| **Pass rate** | **12/20 (60%)** |
| Mean score (PASS=100, SOME=50, FAIL=0, SKIP=0) | 67.5 |
| Catastrophic tasks | 1 |
| Median position error (mm, tasks that ran) | 3.4 |
| Median angle error on turned cubes (deg) | 25.6 |

| Group | Pass rate |
|---|---|
| A: moves | 5/5 (100%) |
| B: swaps with a turn | 0/5 (0%) |
| C: towers of two | 3/5 (60%) |
| D: tower of three, drops | 4/5 (80%) |

Failures by type (SOME PARTS included): execution 5, plan 3. **No controller alarms** this study (the arm's joint-limit
model from Update 2 held).

### Task by task

| Task | Group | Instruction | Outcome | Notes |
|---|---|---|---|---|
| S-01 | A | Move the red cube 40 mm further from the robot. | PASS | |
| S-02 | A | Move the blue cube 40 mm nearer the robot. | PASS | |
| S-03 | A | Move the green cube 50 mm further from the robot. | PASS | |
| S-04 | A | Move the green cube 50 mm nearer the robot. | PASS | |
| S-05 | A | Move the red cube 40 mm nearer the robot and the blue cube 40 mm further from the robot. | PASS | |
| S-06 | B | Swap the red and green cubes, then turn the red cube 45 degrees anticlockwise. | SOME PARTS | execution, 3.9 mm position error, 25.6° angle miss |
| S-07 | B | Swap the red and blue cubes, then turn the blue cube 30 degrees anticlockwise. | FAIL | execution, 122.7 mm |
| S-08 | B | Swap the green and blue cubes, then turn the green cube 45 degrees clockwise. | SOME PARTS | execution, 3.1 mm |
| S-09 | B | Swap the blue and red cubes, then turn the red cube 30 degrees clockwise. | SOME PARTS | execution, 5.9 mm |
| S-10 | B | Swap the red and blue cubes, then turn both of them 30 degrees clockwise. | FAIL | execution, 189.8 mm |
| S-11 | C | Put the red cube on the green cube. | PASS | |
| S-12 | C | Take the red cube off the green cube and put it to the right of the green cube with a 50 mm gap. | PASS | |
| S-13 | C | Put the blue cube on the green cube. | PASS | |
| S-14 | C | Take the tower apart: put the blue cube to the left of the green cube with a 45 mm gap. | FAIL | plan, 70.0 mm |
| S-15 | C | Put the green cube on the blue cube. | FAIL | plan, 50.7 mm |
| S-16 | D | Take the green cube off the blue cube and put it to the right of the blue cube with a 40 mm gap. | PASS | |
| S-17 | D | Build a tower with the green cube at the bottom, then the red cube, then the blue cube on top. | PASS | |
| S-18 | D | Take the blue cube off the tower and put it to the left of the tower with a 60 mm gap. | PASS | |
| S-19 | D | Take the red cube off the green cube, lift it 50 mm above the table to the right of the green cube with a 50 mm gap, and let it drop. | PASS | |
| S-20 | D | Pick up the blue cube, lift it 40 mm above the table, move it 40 mm nearer the robot, and let it drop. | FAIL · catastrophic | plan; blue cube knocked off the table |

### Note on SOME PARTS

The three Group B SOME PARTS runs (S-06, S-08, S-09) all missed on angle, not position — the fingers angle check at
15° was discarding its own measurement when the gripper's mounting offset was ~20°. This is the finding that drove
Update 3.

## What changed after Study 3

Narration v3: the update after Study 3 (V4.5, extending V4.4). Full account: `Kyozo_Link/study/NARRATION_v3.md`;
every change: `Kyozo_Link/study/CHANGES_v3.csv` (9 changes). See `../../A1_version_diffs.md` for the grouped diff.

Key changes:
- The fingers angle check now accepts offsets up to 30° (was 15°), with a log note above 15°. **This is the change
  that let the arm correct for the ~20° wrist-mounted gripper offset — Study 4's angle error dropped from 25.6° to
  11.9°.**
- A turn counts from how the cube lay when the request began (noted at the first look).
- A cube just put down may be picked at the recorded put-down angle rather than refused for an unsteady reading.
- New tool `drop(height_mm=…)` added (26 tools total; existing 25 unchanged in name and signature).
- A cube under another, seen only by its sides, is named from the colour groups with the top's group left out.
- "X on Y" where Y stands on X: Y is put back where it stood, then X is put on it (the pair stays where the pile was).
- Twin: what the fingers touch is judged where they really point, matching the arm's actual grip.
