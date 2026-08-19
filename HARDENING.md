<!-- markdownlint-disable -->

# Hardening Report: mschilde--auto-label-merge-conflicts/v2.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **mschilde--auto-label-merge-conflicts/v2.0** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

Both workflow files reference GitHub Actions using mutable tags or branch names instead of pinned full-length SHA commit hashes, making them vulnerable to supply-chain attacks if the referenced action is compromised or altered.

- `.github/workflows/label.yml` line 7: `uses: actions/labeler@v2` (tag ref)
- `.github/workflows/label_merge_conflicts.yml` line 9: `uses: mschilde/auto-label-merge-conflicts@master` (branch ref)

Locations:

- `.github/workflows/label.yml:7`
- `.github/workflows/label_merge_conflicts.yml:9`

### missing-permissions (severity: medium)

Neither workflow file declares a `permissions:` block at the top level or at the job level. Without explicit permissions, workflows run with the default (potentially broad) token permissions. Both files should declare minimal required permissions.

- `.github/workflows/label.yml`: no `permissions:` key found
- `.github/workflows/label_merge_conflicts.yml`: no `permissions:` key found

Locations:

- `.github/workflows/label.yml:1`
- `.github/workflows/label_merge_conflicts.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed both workflow files:
1. `.github/workflows/label.yml`: Pinned `actions/labeler@v2` to full SHA `5f867a63be70efff62b767459b009290364495eb` and added `permissions: {contents: read, pull-requests: write}` at the top level.
2. `.github/workflows/label_merge_conflicts.yml`: Pinned `mschilde/auto-label-merge-conflicts@master` to full SHA `3fdaf1c8b3f8e5b0f88753d9cb3c9c779370b3ef` and added `permissions: {contents: read, pull-requests: write}` at the top level. Both actions need pull-requests: write to apply labels and contents: read as a baseline.

