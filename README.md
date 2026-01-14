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

feature-auth -> main
https://github.com/user/repo/pull/42
   feature-auth-tests -> feature-auth
   https://github.com/user/repo/pull/43

   feature-auth-oauth -> feature-auth [DRAFT]
   https://github.com/user/repo/pull/44
      feature-auth-oauth-google -> feature-auth-oauth
      https://github.com/user/repo/pull/45

feature-dashboard -> main
https://github.com/user/repo/pull/46
```

Shows all open PRs (including drafts) in a stacked structure based on their base branches.

- `head -> base` shows branch relationship
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
feature-auth -> main
https://github.com/user/frontend/pull/42

[backend]
feature-auth -> main
https://github.com/user/backend/pull/15

fix/api-bug -> main
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

feature-auth -> main
https://github.com/user/frontend/pull/42
https://github.com/user/backend/pull/15

fix/api-bug -> main
https://github.com/user/backend/pull/16
```
