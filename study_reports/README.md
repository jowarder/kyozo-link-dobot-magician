# Kyozo Link: study reports (studies 1-4)

Results of the Simple 20 tasks (three 25 mm cubes, 20 chained tasks in four groups) run by Kyozo Link: a local
language model (Qwen) driving a Dobot Magician from a depth camera, scored by the watcher's own camera. Studies 1 and
2 also ran in the digital twin (a simulation with ideal hardware). After each study the software was improved from
that study's results, and the next study ran on the improved version.

- **Rafiul Azim Jowarder**, Doctoral Student, Victor A. Zaloom Department of Industrial and Systems Engineering,
  Lamar University
- Supervisor: **Dr. James Curry**, Chair and Professor, Victor A. Zaloom Department of Industrial and Systems
  Engineering, Lamar University
- With help from **Wenhao Yang, Ph.D.**, Assistant Professor, Victor A. Zaloom Department of Industrial and Systems
  Engineering, Lamar University

## All studies

Each study is reported as **20 tasks**, one outcome per task, under the frozen V4.5 scorer. When a task was attempted
more than once in a study (reruns, retries after a skipped first attempt), the task's outcome is the **best of its
attempts** (PASS > SOME PARTS > FAIL > SKIPPED). Study 2 had an aborted first sitting (lost USB link, controller stuck
in alarm `0x12` after S-05) and a complete second sitting; per the pre-registration only the second sitting is counted
here. See `METHODOLOGY.md` for the full rule.

| Study | Data | Dates | Version | Tasks | PASS | SOME PARTS | FAIL | SKIPPED | **Pass rate** | Mean score | Catastrophic tasks |
|---|---|---|---|---|---|---|---|---|---|---|---|
| [1](study_1/REPORT.md) | Real Dobot Magician | 2026-10-23 | V4.1 (base) | 20 | 10 | 0 | 5 | 5 | **50 %** | 50.0 | 0 |
| [1](study_1/REPORT.md) | Digital twin | 2026-10-23 | V4.1 (base) | 20 | 4 | 0 | 1 | 15 | **20 %** | 20.0 | 0 |
| [2](study_2/REPORT.md) | Real Dobot Magician (2nd sitting) | 2026-10-26 | V4.3 (v1) | 20 | 4 | 0 | 16 | 0 | **20 %** | 20.0 | 5 |
| [2](study_2/REPORT.md) | Digital twin | 2026-10-25 | V4.3 (v1) | 20 | 19 | 0 | 1 | 0 | **95 %** | 95.0 | 0 |
| [3](study_3/REPORT.md) | Real Dobot Magician | 2026-10-28 | V4.4 (v2) | 20 | 12 | 3 | 5 | 0 | **60 %** | 67.5 | 1 |
| [4](study_4/REPORT.md) | Real Dobot Magician | 2026-10-28 | V4.5 (v3) | 20 | 13 | 3 | 4 | 0 | **65 %** | 72.5 | 2 |

Pass rate on the real Dobot, by group (strict pass, best of attempts, 5 tasks per group):

| Study | A: moves | B: swaps with a turn | C: towers of two | D: tower of three, drops |
|---|---|---|---|---|
| 1 | 4/5 (80%) | 1/5 (20%) | 5/5 (100%) | 0/5 (0%) |
| 2 | 4/5 (80%) | 0/5 (0%) | 0/5 (0%) | 0/5 (0%) |
| 3 | 5/5 (100%) | 0/5 (0%) | 3/5 (60%) | 4/5 (80%) |
| 4 | 5/5 (100%) | 2/5 (40%) | 4/5 (80%) | 2/5 (40%) |

### Base vs V3 on the 15 shared tasks (S-01 to S-15)

Dr. Yang's cross-check metric. On the 15 tasks that every study ran:

| Measure | Study 1 (base, V4.1) | Study 4 (v3, V4.5) |
|---|---|---|
| Pass count (strict) | 10/15 | 11/15 |
| Mean score (PASS=100, SOME=50, FAIL=0) | 66.7 | 83.3 |

McNemar on paired strict pass (b=2, c=3): **p = 1.0** — the pass-count change is not statistically significant on one
run per task per study.
Paired Wilcoxon on continuous score (n=7 non-zero differences): **p ≈ 0.27** — also not statistically significant.

The paper reports these honestly in Limitations and leads on the measured quantities whose change is substantial
(angle error 27.6° → 11.9°; refused steps per run 0.65 → 0.30; catastrophic events 5 → 1 → 2 after Update 2;
twin-forecast gap 75 → 40 → 25 points).

## How it is counted

- **One outcome per task.** The frozen V4.5 scorer scored every attempt; this report collapses multiple attempts of
  the same task to one outcome per task by "best of attempts" (PASS > SOME PARTS > FAIL > SKIPPED).
- **SKIPPED counts as a FAIL** for the pass rate. A SKIPPED task is one where no attempt ever ran (Study 1's Group D).
- **SOME PARTS counts as a FAIL** for strict pass rate (per the pre-registration: a pass needs every target within
  10 mm and 8°, and no other cube moved more than 10 mm). SOME PARTS still carries a 0-100 partial score beside it.
- **Mean score** is PASS = 100, SOME PARTS = 50, FAIL = 0, SKIPPED = 0, averaged over the 20 tasks.
- **Catastrophic tasks** is the number of tasks that had at least one catastrophic attempt (cube off the table, cube
  not in the task moved more than 30 mm, tower brought down, arm couldn't park). Study 2's catastrophic count comes
  from the second sitting only.

## What is here

| File | What |
|---|---|
| `README.md` | This page: all four studies side by side |
| `METHODOLOGY.md` | The collapse rule in full, the frozen scorer's hashes, and how to reproduce the numbers |
| `all_studies.xlsx` | The same overview, and every attempt of every study in one sheet |
| `study_N/REPORT.md` | One study: setup, results, task by task (one row per task), every failed or skipped attempt, what changed after it |
| `study_N/study_N.xlsx` | The same as sheets: summary, attempts, tasks, changes made after the study |

## Sources

- The watcher's packages `Kyozo_Link_Results/For_Claude/study_1` to `study_4` (`full_report.json`; study 1's tasks
  skipped before V4.2 from `skipped_before_v4.2.json`).
- The tasks: `Kyozo_Link/study/tasks/simple.yaml`. The changes after each study: `Kyozo_Link/study/CHANGES_vN.csv` and
  `NARRATION_vN.md`. The study plan: `Kyozo_Link/study/PREREG.md`.
- Left out: pictures, depth files and raw run folders (too large for GitHub, and the study's raw data), practice
  sessions (not counted), and the unseen test set and its results (kept private).
