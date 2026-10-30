# Version history

Python lines count every `.py` file at the version's git tag,
including the watcher, tests and test scripts.

| Version | Date   | Working state reached                                              | Python lines | Tests |
|---------|--------|--------------------------------------------------------------------|--------------|-------|
| Start   | 11 Sep | Nameplate photo, project goals and a few commands                  | —            | —     |
| V1.8    | 23 Sep | First on the robot, with camera, calibration, 12 tools (Qwen3-8B)  | 11,803       | 127   |
| V2.1    | 29 Sep | Depth detector, two-finger grasp planner, packing planner          | 19,122       | 231   |
| V3.5    | 4 Oct  | Renamed Kyozo Link, Qwen3-4B planner, multi-object tools           | 27,574       | 379   |
| V3.6    | 8 Oct  | Cube calibration with no marker                                    | 33,571       | 437   |
| V3.7    | 9 Oct  | Fingers angle check                                                | 36,325       | 467   |
| V3.8    | 13 Oct | Watcher and the 20 test tasks                                      | 50,127       | 631   |
| V4.0    | 22 Oct | Continuous calibration, pydobot checksum fix                       | 57,599       | 744   |
| V4.1    | 23 Oct | Round 1, the baseline                                              | 60,083       | 768   |
| V4.3    | 26 Oct | Round 2, after Update 1                                            | 63,706       | 817   |
| V4.4    | 28 Oct | Round 3, after Update 2                                            | 65,374       | 867   |
| V4.5    | 28 Oct | Round 4, after Update 3                                            | 65,898       | 880   |

All dates are in 2026.

Only the V4.6 code is bundled in this repository. Earlier tags were
used during development to measure growth but have not been pushed;
the counts above are from `wc -l` on each local tag.

This table matches Table II of the GECA 2027 submission.
