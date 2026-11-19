# All 17 stacked PR accessibility audit UI paths

These are real native GitHub PR fixtures, not mock screens. The branch and stack relationships are verified through the API. Signed-in browser controls and their exact labels have not been visually verified by this session.

## Accounts

- Main account: Admin, for settings and the scenario 11 bypass test.
- gigachad25: Write is sufficient for reviews and ordinary PR actions. It must not be in a bypass list.
- The access API reported gigachad25 as `read` when this guide was published. Use Settings > Collaborators and teams > Add people > gigachad25 > Write, then accept the invitation while signed in as gigachad25. If access is already Write, no change is needed.
- All fixture PRs were created by the signed-in main account. Use gigachad25 to approve them; the PR author cannot approve their own PR.

## Readiness

Fixtures are prepared for every row below. Rules, auto-merge settings, and workflow installation are only ready where explicitly verified. A repository Admin role does not automatically grant this session's GitHub App permission to change administration settings.

The session encountered these setup blockers:

- **reviews:** `POST repos/Teamelite12/stacked-pr-audit/rulesets: gh: Resource not accessible by integration (HTTP 403) {"message":"Resource not accessible by integration","documentation_url":"https://docs.github.com/rest/repos/rules#create-a-repository-ruleset","status":"403"}`
- **bypass:** `POST repos/Teamelite12/stacked-pr-audit/rulesets: gh: Resource not accessible by integration (HTTP 403) {"message":"Resource not accessible by integration","documentation_url":"https://docs.github.com/rest/repos/rules#create-a-repository-ruleset","status":"403"}`
- **queue:** `POST repos/Teamelite12/stacked-pr-audit/rulesets: gh: Resource not accessible by integration (HTTP 403) {"message":"Resource not accessible by integration","documentation_url":"https://docs.github.com/rest/repos/rules#create-a-repository-ruleset","status":"403"}`
- **auto-merge-setting:** `PATCH repos/Teamelite12/stacked-pr-audit: gh: Resource not accessible by integration (HTTP 403) {"message":"Resource not accessible by integration","documentation_url":"https://docs.github.com/rest/repos/repos#update-a-repository","status":"403"}`

## Direct UI paths

| # | Scenario | Open URL | Simple UI path | Readiness |
|---|---|---|---|---|
| 1 | Create Stack from Existing PRs | [Open UI](https://github.com/Teamelite12/stacked-pr-audit/pull/2) | Create stack recommendation > preview > confirm. | Fixture prepared |
| 2 | Create Stack with a New PR | [Open UI](https://github.com/Teamelite12/stacked-pr-audit/compare/audit/stacked-20261119/s02/layer-1...audit/stacked-20261119/s02/layer-2?expand=1) | Base/compare selectors > Create pull request > Create stack. | Fixture prepared |
| 3 | Stack Header | [Open UI](https://github.com/Teamelite12/stacked-pr-audit/pull/5) | Stack icon and layer number beside the PR title > stack details. | Fixture prepared |
| 4 | Stack Context in PR List | [Open UI](https://github.com/Teamelite12/stacked-pr-audit/pulls?q=is%3Apr%20is%3Aopen%20S03) | Pull requests > S03 results > stack indicator > stack details and PR links. | Fixture prepared |
| 5 | Stack Map | [Open UI](https://github.com/Teamelite12/stacked-pr-audit/pull/5) | Merge section at the bottom > stack map > PR links and statuses. | Fixture prepared |
| 6 | Stack Keyboard Shortcuts | [Open UI](https://github.com/Teamelite12/stacked-pr-audit/pull/5) | Shift+J / Shift+K > destination PR heading and layer. | Fixture prepared |
| 7 | Add to Stack | [Open UI](https://github.com/Teamelite12/stacked-pr-audit/pull/8) | Stack icon > Add to stack > branch selector > PR form. | Fixture prepared |
| 8 | Rebase Stack | [Open UI](https://github.com/Teamelite12/stacked-pr-audit/pull/11) | Merge section > Rebase stack > confirmation > status. | Fixture prepared; administrator setup needed |
| 9 | Stack Merge Requirements | [Open UI](https://github.com/Teamelite12/stacked-pr-audit/pull/14) | Merge section > required approval message > review details and blocked merge control. | Fixture prepared; administrator setup needed |
| 10 | Merge Stack | [Open UI](https://github.com/Teamelite12/stacked-pr-audit/pull/17) | Merge section > included PRs > merge method > confirmation. | Fixture prepared |
| 11 | Bypass Stack Merge Requirements | [Open UI](https://github.com/Teamelite12/stacked-pr-audit/pull/19) | Lowest PR > merge restriction > bypass option > confirmation. | Fixture prepared; administrator setup needed |
| 12 | Stack Merge Queue | [Open UI](https://github.com/Teamelite12/stacked-pr-audit/pull/23) | Merge when ready > confirmation > queued status > merge queue link > merge-group details. | Fixture prepared; administrator setup needed |
| 13 | Stack Auto-merge | [Open UI](https://github.com/Teamelite12/stacked-pr-audit/pull/26) | Contiguous PR-group selection > auto-merge > confirmation > status/cancel. | Fixture prepared; administrator setup needed |
| 14 | Partial Merge and Automatic Retargeting | [Open UI](https://github.com/Teamelite12/stacked-pr-audit/pull/28) | Merge bottom PR only > open upper PR > updated base and stack position. | Fixture prepared |
| 15 | Branching Stack Retargeting | [Open UI](https://github.com/Teamelite12/stacked-pr-audit/pull/34) | Merge parent bottom PR > delete its audit-only branch > dependent bottom PR > base and activity. | Fixture prepared |
| 16 | Stack Membership Timeline | [Open UI](https://github.com/Teamelite12/stacked-pr-audit/pull/37) | PR activity timeline > added-to-stack and removed-from-stack events. | Fixture prepared |
| 17 | Unstack Pull Requests | [Open UI](https://github.com/Teamelite12/stacked-pr-audit/pull/41) | Stack options > Unstack > confirmation > remaining PRs and base branches. | Fixture prepared |

## One-time administrator configuration

Open URL: https://github.com/Teamelite12/stacked-pr-audit/settings/rules

Path: Settings > Rules > Rulesets > New ruleset > Import a ruleset. Download each JSON file linked below, import it, confirm the exact audit-only branch targets, and save it as Active. Do not replace an existing ruleset or target main/all branches.

- [Stack audit - reviews](https://github.com/Teamelite12/stacked-pr-audit/blob/main/audit/stacked-pr/setup/reviews.json): targets `audit/stacked-20261119/rebase-base`, `audit/stacked-20261119/requirements-base`, `audit/stacked-20261119/auto-base`.
- [Stack audit - bypass](https://github.com/Teamelite12/stacked-pr-audit/blob/main/audit/stacked-pr/setup/bypass.json): targets `audit/stacked-20261119/bypass-base`.
- [Stack audit - queue](https://github.com/Teamelite12/stacked-pr-audit/blob/main/audit/stacked-pr/setup/queue.json): targets `audit/stacked-20261119/queue-base`.

The reviews ruleset requires one approval and dismisses stale approvals; it has no bypass actors. The bypass ruleset requires one approval and grants the Repository admin role bypass For pull requests only. The queue ruleset requires the `Audit fixture check` status and a merge queue, without required approvals.

### Workflow approval

The initial PR workflow runs report Action required and are awaiting maintainer approval. The run-approval API could not approve these same-repository runs. As the main account, open the PR's Checks area or Actions > Stack audit checks > the relevant run, review the workflow, and use Approve and run workflows if displayed. Approve both S12 PR runs before enqueueing the stack. If the control is absent, use the displayed approval explanation or ask the organization administrator. Do not treat Action required as a passing check.

For scenario 13: open https://github.com/Teamelite12/stacked-pr-audit/settings > General > Pull Requests > enable Allow auto-merge. Keep Automatically delete head branches disabled until the branching-retargeting audit.

### Workflow

The workflow is supplied at [setup/audit-checks.yml](setup/audit-checks.yml). If it was not installed automatically, use Add file > Create new file on main and create `.github/workflows/audit-checks.yml` with that exact content. Commit it using the main account.

Existing fixtures need the workflow in their commit history too. If installation was blocked, finish that step before running the queue scenario and have the setup agent refresh the audit bases and cascade the affected branches. Do not select a required check that has never run.

The workflow validates the audit fixture files. On merge_group it waits 180 seconds before passing, which provides time to open queue and merge-group details. The queue may merge immediately afterwards. Remove the stack from the queue if you are not ready for the merge.

## Per-scenario remarks

### 1. Create Stack from Existing PRs

Open URL: https://github.com/Teamelite12/stacked-pr-audit/pull/2

Path: Create stack recommendation > preview > confirm.

Remarks: Two dependent PRs are intentionally unstacked. Complete creation during the audit.

### 2. Create Stack with a New PR

Open URL: https://github.com/Teamelite12/stacked-pr-audit/compare/audit/stacked-20261119/s02/layer-1...audit/stacked-20261119/s02/layer-2?expand=1

Path: Base/compare selectors > Create pull request > Create stack.

Remarks: The lower PR already exists. The upper branch is pushed without a PR. Base: `audit/stacked-20261119/s02/layer-1`; compare: `audit/stacked-20261119/s02/layer-2`.

### 3. Stack Header

Open URL: https://github.com/Teamelite12/stacked-pr-audit/pull/5

Path: Stack icon and layer number beside the PR title > stack details.

Remarks: Native two-PR stack; use the persistent header on the same page.

### 4. Stack Context in PR List

Open URL: https://github.com/Teamelite12/stacked-pr-audit/pulls?q=is%3Apr%20is%3Aopen%20S03

Path: Pull requests > S03 results > stack indicator > stack details and PR links.

Remarks: The native stack indicator belongs to the S03 fixtures.

### 5. Stack Map

Open URL: https://github.com/Teamelite12/stacked-pr-audit/pull/5

Path: Merge section at the bottom > stack map > PR links and statuses.

Remarks: Use the same native stack as scenario 3.

### 6. Stack Keyboard Shortcuts

Open URL: https://github.com/Teamelite12/stacked-pr-audit/pull/5

Path: Shift+J / Shift+K > destination PR heading and layer.

Remarks: Navigate in both directions. The two PRs provide the stack boundaries.

### 7. Add to Stack

Open URL: https://github.com/Teamelite12/stacked-pr-audit/pull/8

Path: Stack icon > Add to stack > branch selector > PR form.

Remarks: Choose `audit/stacked-20261119/s07/layer-3`. It is pushed and does not have a PR.

### 8. Rebase Stack

Open URL: https://github.com/Teamelite12/stacked-pr-audit/pull/11

Path: Merge section > Rebase stack > confirmation > status.

Remarks: The base has an independent additional commit. For approval retention, first configure the reviews rule and approve both PRs as gigachad25. Then rebase as the main account and inspect retained approvals and replacement commit signatures. Do not use Update branch instead.

### 9. Stack Merge Requirements

Open URL: https://github.com/Teamelite12/stacked-pr-audit/pull/14

Path: Merge section > required approval message > review details and blocked merge control.

Remarks: Configure the reviews ruleset first. Leave both PRs unapproved to preserve the restriction.

### 10. Merge Stack

Open URL: https://github.com/Teamelite12/stacked-pr-audit/pull/17

Path: Merge section > included PRs > merge method > confirmation.

Remarks: Merge the upper PR only during the approved audit to merge both layers into the isolated merge-base.

### 11. Bypass Stack Merge Requirements

Open URL: https://github.com/Teamelite12/stacked-pr-audit/pull/19

Path: Lowest PR > merge restriction > bypass option > confirmation.

Remarks: Configure the bypass ruleset first. Use the main Admin account; keep the required approval missing. Do not use the upper PR.

### 12. Stack Merge Queue

Open URL: https://github.com/Teamelite12/stacked-pr-audit/pull/23

Path: Merge when ready > confirmation > queued status > merge queue link > merge-group details.

Remarks: Configure the queue rule and working required check first. Select both layers. The prepared workflow supports pull_request and merge_group; its queue job pauses for 180 seconds so the queue details can be inspected before merging.

### 13. Stack Auto-merge

Open URL: https://github.com/Teamelite12/stacked-pr-audit/pull/26

Path: Contiguous PR-group selection > auto-merge > confirmation > status/cancel.

Remarks: Configure the reviews rule and enable Allow auto-merge first. Leave approvals missing until after the enabled/cancel state is audited. If the stack-specific auto-merge UI is absent, mark blocked rather than substituting single-PR auto-merge.

### 14. Partial Merge and Automatic Retargeting

Open URL: https://github.com/Teamelite12/stacked-pr-audit/pull/28

Path: Merge bottom PR only > open upper PR > updated base and stack position.

Remarks: After merging the bottom PR, open https://github.com/Teamelite12/stacked-pr-audit/pull/29. Do not merge the upper PR; inspect automatic retargeting and status.

### 15. Branching Stack Retargeting

Open URL: https://github.com/Teamelite12/stacked-pr-audit/pull/34

Path: Merge parent bottom PR > delete its audit-only branch > dependent bottom PR > base and activity.

Remarks: First merge https://github.com/Teamelite12/stacked-pr-audit/pull/31 and delete only `audit/stacked-20261119/s15p/layer-1`. Then inspect this dependent PR. If it retargets to main, do not merge it into main.

### 16. Stack Membership Timeline

Open URL: https://github.com/Teamelite12/stacked-pr-audit/pull/37

Path: PR activity timeline > added-to-stack and removed-from-stack events.

Remarks: Both event types already exist on this fixture. For an active added-membership link, also use https://github.com/Teamelite12/stacked-pr-audit/pull/5. Use the activity stream if Conversation is absent.

### 17. Unstack Pull Requests

Open URL: https://github.com/Teamelite12/stacked-pr-audit/pull/41

Path: Stack options > Unstack > confirmation > remaining PRs and base branches.

Remarks: The dedicated native stack is open, unmerged, and unqueued. Unstack only during the audit.

## Audit safety

Merge, rebase, auto-merge, and unstack actions are intentionally left for the auditor. The separate S16 fixture was already unstacked to create real removal events. All destructive fixture actions target disposable audit branches. Never change their destination to main. Branch deletion in scenario 15 may retarget dependent PRs to main; inspect but do not merge them there.

Do not approve S09, S11, or S13 until their missing-approval, bypass, or auto-merge state is audited. For S08, have gigachad25 approve both layers before the main account rebases.

End each scenario with: Verify whether step 2, 3 and 4 are accessible and WCAG compliant or not.
