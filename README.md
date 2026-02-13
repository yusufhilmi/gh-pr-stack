# gh-pr-stack

Visualize stacked pull requests in a tree format.

> **Note:** This command works within a single repository. It does not cover multiple repos at this time.

## Installation

```bash
gh extension install yusufhilmi/gh-pr-stack
```

## Usage

Run this command inside a git repository:

```bash
gh pr-stack
```

## Example Output

```
OPEN PR STACKS

+145 −23 (8 files)
main <- feature-auth
https://github.com/user/repo/pull/42
   +67 −12 (4 files)
   feature-auth <- feature-auth-tests
   https://github.com/user/repo/pull/43

   +234 −89 (12 files)
   feature-auth <- feature-auth-oauth [DRAFT]
   https://github.com/user/repo/pull/44
      +45 −3 (2 files)
      feature-auth-oauth <- feature-auth-oauth-google
      https://github.com/user/repo/pull/45

+89 −34 (6 files)
main <- feature-dashboard
https://github.com/user/repo/pull/46
```

Shows all open PRs (including drafts) in a stacked structure based on their base branches.

- `+additions −deletions (files changed)` shows diff statistics
  - Green for additions
  - Red for deletions
  - Orange for file count
- `base <- head` shows branch relationship (matching GitHub UI)
  - Purple for base branch
- Draft PRs are marked with `[DRAFT]`
- Indentation shows PR dependencies
- Empty lines separate sibling branches and root-level stacks

## TODO - Multi-repo Support

Since I prefer monorepos, didnt implement this but if you feel like it, feel free to contribute.

Include PRs from other repositories (same owner):

```bash
gh pr-stack --include backend,frontend
gh pr-stack --include backend frontend
```

Include repos from different owners:

```bash
gh pr-stack --include other-org/repo
```

### Unified View

```bash
gh pr-stack --include backend,frontend
```

```
OPEN PR STACKS

[frontend]
+120 −45 (7 files)
main <- feature-auth
https://github.com/user/frontend/pull/42

[backend]
+89 −23 (5 files)
main <- feature-auth
https://github.com/user/backend/pull/15

+12 −8 (2 files)
main <- fix/api-bug
https://github.com/user/backend/pull/16
```

### Multi-repo (with --match)

Use `--match` to group PRs with matching branch names across repos:

```bash
gh pr-stack --include backend,frontend --match
```

```
OPEN PR STACKS

[UNIFIED frontend backend]

+120 −45 (7 files)
main <- feature-auth
https://github.com/user/frontend/pull/42
+89 −23 (5 files)
main <- feature-auth
https://github.com/user/backend/pull/15

+12 −8 (2 files)
main <- fix/api-bug
https://github.com/user/backend/pull/16
```
