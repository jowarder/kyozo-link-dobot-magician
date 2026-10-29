# Methodology — how the reports were produced

## The frozen scorer

All four studies were (re-)scored under the same code: `Kyozo_Link/watcher/` and `Kyozo_Link/study/` at git commit `26ea23e` (the V4.5 release plus the V4.6 development work in progress on 2026-10-29). The SHA-256 of every watcher module at that commit:

| File | SHA-256 |
| --- | --- |
| `__init__.py` | `083c87d042dfad4d44df8105f569e8e6ae34670b4c7ad1820c14211aad19120a` |
| `arrange.py` | `361a453a5acbf0759d3fb796f9c040f9683ff8c71ea4f3b312b639823ef59f66` |
| `details.py` | `444ccc0af922f349cc9dce3a62700d4aa87cdc44f1e26a3028ee513266f5661e` |
| `extract.py` | `9687fa0944e54508e6c84e5f05255c52085f56ef097d6faa88facde5fa2eb747` |
| `finder.py` | `5918dcc371c22f02787fd61d1df3cd4bd8be8224d92b9c305fce531912824dc1` |
| `ghost.py` | `8d07e8e7092adba7440a76d8ad8ecd504fd9bf90d022f61315514f8db32a82a2` |
| `handoff.py` | `84be88b92eba197861529fa0d12aaf83c5f919d9e82cdeb01f2d783ddab096f3` |
| `model_log.py` | `7812e5654a9a81a36cf9a6a9f70ce561df8fa2563e558d3e48dad7dcf52c2bed` |
| `observe.py` | `1c11dad38e1765165f588788a58cd79cd19e773c7bc4e2024c1529dbe5295ec9` |
| `overview.py` | `bd4b3dc692ec832ec31c33281c0125301161be9a4915ec1e710e89a21b5e0d18` |
| `prompt_record.py` | `31ac7e18fbbbaecec089c65a2e8caefef7338081b01332e081118e49dfc7224b` |
| `report.py` | `a8ba627193793be25374ba2a739b390e82202d714d2d6ce84cc3e6cb13b37419` |
| `results.py` | `8458556b275dd9e6061c7affee1094934ad80a19c48d446a4e682ed149047a8e` |
| `setout.py` | `cfba16e67c5fd4b39d4b2c9d6750960d298449aaac2c627452ca59a9bce21416` |
| `status_strip.py` | `5b04294ff804ce2b522a3dee2eaae620bc35cd7ecc83b825386a7b7315cc930a` |
| `tasks.py` | `3bd54a473584fb00ac3e27415c0315bf1a996109a450eda311f9767241ae3705` |
| `taxonomy.py` | `fe220d511c555beddff69fe471791d0ff6aaacfc1c04af3ce5ae80fd8694ec4c` |
| `tour.py` | `77827cc454d1ba3a56289e6b967c5b4be9f077b89bba26597e8ab38926d2e9b2` |
| `window.py` | `e16deffb813cfafcdd0e9c40b8d771b24a90412e90b91c6c0ad0e461fdaff9b5` |

## The collapse rule — one outcome per task

Each study is reported as 20 tasks, one row per task. When a task was attempted more than once in a study, its outcome is the **best of its attempts**:

> **PASS > SOME PARTS > FAIL > SKIPPED**

A SKIPPED task is one where no attempt ever ran (the watcher never started it because the camera did not see the table ready for it). A task that ran at least once can be at best FAIL, if no attempt met any target.

### Study 2 — the two sittings

Study 2 had an aborted first sitting (`2026-10-26_123244`, stopped by lost USB link and a stuck `0x12` alarm after S-05) and a complete second sitting (`2026-10-26_180835`). The pre-registration (`Kyozo_Link/study/PREREG.md`) states that an interrupted sitting is retried, and only the complete sitting is reported.

Here that means:

- S-01 through S-12: both sittings attempted the task; the outcome is taken from the **second sitting** (its Run2 for these tasks).
- S-13 through S-20: the first sitting was already aborted; the only attempt is from the **second sitting** (its Run1 for these tasks).

Study 2's catastrophic count is the number of second-sitting tasks that had a catastrophic attempt (5 tasks: S-07, S-09, S-11, S-12, S-19).

## Mean score

PASS = 100, SOME PARTS = 50, FAIL = 0, SKIPPED = 0, averaged over the 20 tasks:

- Study 1: (10 × 100 + 0 × 50 + 5 × 0 + 5 × 0) / 20 = **50.0**
- Study 2: (4 × 100 + 0 × 50 + 16 × 0 + 0 × 0) / 20 = **20.0**
- Study 3: (12 × 100 + 3 × 50 + 5 × 0 + 0 × 0) / 20 = **67.5**
- Study 4: (13 × 100 + 3 × 50 + 4 × 0 + 0 × 0) / 20 = **72.5**

## Mean score, 15 shared tasks (S-01 to S-15)

The 15 tasks every study scored (Study 1 skipped S-16 to S-20 due to a watcher camera-view bug; the paper's Section V-A explains):

- Study 1: 10 PASS + 0 SOME + 5 FAIL = (10 × 100 + 5 × 0) / 15 = **66.7**
- Study 2: 4 PASS + 0 SOME + 11 FAIL = (4 × 100) / 15 = **26.7**
- Study 3: 8 PASS + 3 SOME + 4 FAIL = (8 × 100 + 3 × 50) / 15 = **63.3**
- Study 4: 11 PASS + 3 SOME + 1 FAIL = (11 × 100 + 3 × 50) / 15 = **83.3**

## Statistical tests on base vs V3 (15 shared tasks)

**McNemar on paired strict pass.** Pass in both: 8 (S-01, S-02, S-03, S-04, S-11, S-12, S-13, S-15). Pass only in base: 2 (S-10, S-14). Pass only in V3: 3 (S-05, S-06, S-09). Both fail: 2 (S-07, S-08; both are SOME PARTS in V3 which still counts as non-pass for strict). McNemar statistic (|b−c|−1)²/(b+c) = 0 / 5 = 0, chi-squared one df, two-tailed **p = 1.0**.

**Paired Wilcoxon signed-rank on continuous score.** Per-task score differences (Study 4 − Study 1): 7 non-zero (five positive, two negative). W = 7.5, n = 7, normal approximation z ≈ −1.10, two-tailed **p ≈ 0.27**.

Neither test rejects the null at α = 0.05 on these sample sizes. The paper owns this in its Limitations section.

## Reproducing from the raw data

To reproduce the per-attempt outcomes:

```bash
# Install dependencies in a conda env (NumPy/OpenCV/SciPy/PyBullet)
conda env create -f environment.yml
conda activate dobot_vision

# Re-run the frozen scorer against each study's raw data
python -m study.rescore_v45  study_1/20_Tasks_for_Dobot/_raw_data  -o rescored/study_1.json
python -m study.rescore_v45  study_2/20_Tasks_for_Dobot/_raw_data  -o rescored/study_2.json
# ... etc.
```

The collapse step (per-attempt → per-task) is a small script that reads the rescored JSON and applies Rule A above. Both scripts are in `Kyozo_Link/study/` at the frozen commit.

## What this release does not include

Pictures, depth files, raw run folders (too large for GitHub), practice sessions (not counted), and the unseen test set and its results (kept private per the pre-registration). The paper and this release do not use the unseen test; it is kept for follow-up work.
