# Stacked Pull Request Accessibility Audit

Test repository for the 17 GitHub stacked pull request accessibility scenarios.

## Setup status

The audit branches, pull requests, native stacks, and workflow are prepared.
Repository rules, auto-merge, workflow approvals, and account access must be
completed or confirmed using the guide linked below.

## Test accounts

- Main account: repository administrator; configures rules and tests bypass.
- `gigachad25`: collaborator with Write access; reviews and approves test PRs.

The test account must accept any repository invitation before reviewing.
PR authors cannot approve their own PRs.

## Scenarios

| # | Scenario | Required test setup |
|---|---|---|
| 1 | Create Stack from Existing PRs | Two dependent open PRs, not yet in a native stack. |
| 2 | Create Stack with a New PR | One open PR and a dependent branch without a PR. |
| 3 | Stack Header | An open native stack. |
| 4 | Stack Context in PR List | An open native stack visible in the PR list. |
| 5 | Stack Map | A native stack with at least two PRs. |
| 6 | Stack Keyboard Shortcuts | A native stack with at least two PRs. |
| 7 | Add to Stack | A native stack and a third branch based on its top branch. |
| 8 | Rebase Stack | An outdated stack; reviewer approvals and a stale-approval rule for the approval-retention check. |
| 9 | Stack Merge Requirements | A stack whose audit base requires one approval; leave the PRs unapproved. |
| 10 | Merge Stack | A separate merge-ready stack targeting a disposable audit base. |
| 11 | Bypass Stack Merge Requirements | A stack requiring approval, with the authorized administrator role on the ruleset bypass list. |
| 12 | Stack Merge Queue | A stack targeting an audit base with merge queue enabled and working merge-group checks. |
| 13 | Stack Auto-merge | Auto-merge enabled, an unmet merge requirement, and available stack-specific auto-merge controls. |
| 14 | Partial Merge and Automatic Retargeting | A separate two-PR stack; merge only the bottom PR during the audit. |
| 15 | Branching Stack Retargeting | Two native stacks, with the dependent stack based on a branch belonging to the parent stack. |
| 16 | Stack Membership Timeline | PR activity containing real added-to-stack and removed-from-stack events. |
| 17 | Unstack Pull Requests | A separate native stack with no merged or queued PRs. |

## Repository configuration

- Settings > Collaborators and teams: invite `gigachad25` with Write access.
- Settings > Rules > Rulesets: create separate rules for the relevant audit bases.
- Settings > General > Pull Requests: enable Allow auto-merge for scenario 13.
- Required GitHub Actions checks must support both `pull_request` and
  `merge_group` events for scenario 12.

Keep required approvals missing for scenarios 9, 11, and 13 until their blocked,
bypass, or auto-merge states have been audited. Use the lowest unmerged PR for
scenario 11.

## Audit safety

- Use documentation-only changes and branches under `audit/`.
- Target disposable audit bases, not `main`, for merge tests.
- Keep separate fixtures for full merge, partial merge, branching retargeting,
  membership removal, and unstacking.
- Do not merge the dependent stack into `main` if branch deletion retargets it there.
- Queue and auto-merge actions can merge changes without another confirmation later.
- Confirm private-repository feature availability before execution. Merge queue
  availability depends on the organization's plan; stack auto-merge must also be
  available. Record unavailable features as blocked.

## Audit verification wording

End each scenario with:

> Verify whether step 2, 3 and 4 are accessible and WCAG compliant or not.

Adjust the step numbers when the scenario covers different interaction steps.


## Prepared audit fixtures

[Open all 17 exact UI paths, direct PR links, account roles, and administrator setup](audit/stacked-pr/README.md).

The fixtures are created. Some settings may still require an administrator; see the readiness notes in the guide before executing the audit.
