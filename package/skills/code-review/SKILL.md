---
name: code-review
description: Independently review a current diff against repository standards and task acceptance criteria, reporting only evidenced BLOCKER or MAJOR findings.
---

# Independent code review

Use in a session independent of the author. Read [the review contract](references/review-contract.md). If you authored the change, label your inspection as an author self-check and hand it to the coordinating session for independent review; do not self-certify independence.

1. Resolve exact base/head and inspect the whole requested diff. For a PR, obtain its target and head through available GitHub tools or authorized gh, then compute the merge base. Distinguish staged, working and untracked changes. Without an inspectable diff, report incomplete review.
2. Establish the Spec from the user request, acceptance criteria and pertinent story/ADR. Read selected Trello/Notion sources when available and cite returned URLs/IDs. Missing material context stays an unassessed axis, never a fabricated requirement.
3. Assess Standards (repository contracts, correctness, security, compatibility and checks) separately from Spec (requested behavior). Load relevant project skills. Use Graphify for navigation and deja-vu for pertinent prior decisions only when available; verify mutable facts against code.
4. Run relevant checks in an owned isolated checkout. Reproduce every material finding with a concrete input and observed result. Missing dependencies/access limit the review; do not change the product to make checks pass.
5. Report only demonstrated BLOCKER/MAJOR findings: current file/line, primary axis, concrete impact, reproduction/evidence, minimal correction and verification. Zero findings is legitimate. Cosmetic suggestions and unsupported hypotheticals do not become MR comments.
6. Publish comments only when the current task authorizes them, against the explicit repository and current head. A read-only GitHub MCP cannot publish review; use authorized authenticated gh if available. Do not switch identities or attempt self-approval.
7. Recheck remote head before publication; review new deltas and affected checks. After fixes, rerun the reproducer at the new SHA. After three unresolved rounds, hand the reproducer and disagreement to the coordinator.

Do not merge. Return exact scope, Standards/Spec results, evidence, limitations and whether material findings remain. Passing checks prove their exercised cases, not every requirement.
