# Review contract and origin

Adapted from Smart Harness marketplace/code-review 1.1.1, inspected 2026-10-22. It retains independent review, separate Standards/Spec axes, evidence and current-head verification. The source package records its adaptation from the user's review process 2.0.0. This package carries no personal credentials, private history or standing publication permission.

BLOCKER: demonstrated critical behavior, data-loss risk, security failure or required compatibility break without a migration. MAJOR: demonstrated material defect in behavior, reliability, error handling or verification necessary for this delivery. Severity follows the impact in the actual task.

Each finding includes severity, primary Standards/Spec axis, file/line at reviewed head, reproduction command/input and observed output, impact, minimal correction and a check that can detect the defect. Deduplicate the same defect across axes without losing evidence.

Minimum result: scope/base/head; session independence; sources actually read; checks actually run; Standards and Spec each passed/findings/not assessed; pending BLOCKER/MAJOR findings; limitations; correction required, incomplete review or ready for coordinated acceptance.

No diff or materially missing Spec means incomplete review. An unexecuted check is an explicit limitation. The coordinating session decides merge within the user's authorization.
