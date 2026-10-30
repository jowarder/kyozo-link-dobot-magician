# Kyozo Link

AI-written text-to-robot control software for a Dobot Magician cell with an Orbbec Gemini 335 RGB-D depth camera mounted eye-to-hand. Qwen3-4B plans each request at run time over 25 safety-checked tools, while Claude Opus 5.5 writes and revises the application code offline from an independent watcher’s run records. About 66,000 Python lines total, including the watcher, a PyBullet digital twin, and 880 tests. Four pre-registered studies on real hardware.



This is version **4.6** (git tag `v4.6`, 2026-10-29).

## How this release is laid out

- **Source code** — download **[`Kyozo_Link_V4.6_GitHub.zip`](Kyozo_Link_V4.6_GitHub.zip)** and extract it. Inside the zip:
  the Kyozo Link app's source code, the independent watcher, the digital twin, the tests, the study plan
  (`Kyozo_Link/study/PREREG.md`), Claude's change log (`Kyozo_Link/CHANGELOG.md`), per-update narrations
  (`Kyozo_Link/study/NARRATION_v{1,2,3,4}.md`) and change ledgers (`Kyozo_Link/study/CHANGES_v{1,2,3,4}.csv`).
  Setup instructions are in `Kyozo_Link/README.md` inside the zip.
- **Study results** — browsable directly in this repo: see **[`study_reports/`](study_reports/)**. One Markdown report
  and one Excel workbook per study (studies 1 to 4 on the real Dobot, and studies 1 and 2 in the twin), all four
  side by side in [`study_reports/README.md`](study_reports/README.md), with the frozen scorer's SHA-256 hashes and
  the counting rule in [`study_reports/METHODOLOGY.md`](study_reports/METHODOLOGY.md).

## People

**Rafiul Azim Jowarder**, Doctoral Student, Victor A. Zaloom Department of Industrial and Systems Engineering,
Lamar University.

Supervisor: **Dr. James Curry**, Chair and Professor, Victor A. Zaloom Department of Industrial and Systems
Engineering, Lamar University.

With help from **Wenhao Yang, Ph.D.**, Assistant Professor, Victor A. Zaloom Department of Industrial and Systems
Engineering, Lamar University, Beaumont, TX 77710.

## Counting rule in the study reports

Each study is reported as 20 tasks, one outcome per task (best of attempts). A task the watcher never started counts
as a FAIL. Study 2 reports the complete second sitting (the first sitting was aborted by hardware faults, per the
pre-registration). The full rule and the scorer's hashes are in `study_reports/METHODOLOGY.md`.

## What is not included

Calibration photos, run pictures, depth files and session logs (too large for GitHub, and the study's raw data), and
the unseen test set and its results (kept private per the pre-registration). The per-study `REPORT.md` files describe
every failed and skipped attempt in text; raw run images are available from the authors on request.
