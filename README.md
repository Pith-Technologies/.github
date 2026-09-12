# .github

Organisation-level defaults for Pith Technologies.

This repository is **public by necessity**: a public repository cannot call a
reusable workflow that lives in a private one. It holds no private material.

| Path | Purpose |
|---|---|
| `.github/workflows/private-file-guard.yml` | Reusable workflow that fails when a repository tracks a workspace-private path. Called by every public repo |

## Calling the guard

In each public repository, `.github/workflows/guard.yml`:

```yaml
name: guard
on: [push, pull_request]
jobs:
  guard:
    uses: Pith-Technologies/.github/.github/workflows/private-file-guard.yml@main
```

Then make `guard` a required status check in the organisation ruleset. The
workflow alone reports; the ruleset is what enforces.

## Keeping the patterns in step

The path patterns here mirror `policy/forbidden-paths.txt` in
PithTech-Workspace, which the local git hooks and `ws doctor` read. A pattern
added in one place must be added in the other, or the guard rings disagree
about what is private.
