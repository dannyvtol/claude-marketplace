---
name: commit
description: commit changes as conventional commits, sliced by logical concern
---
# Git commit

A **slice** is one logical concern — a feature, fix, or refactor — regardless of how many files it touches. One file may yield multiple slices.

1. Run `git status --porcelain` and `git diff HEAD` to survey all changes.
2. Identify slices. Every hunk must belong to exactly one slice.
3. For each slice:
   1. Stage its changes: `git add -p` for partial files, `git add <file>` for whole files.
   2. Identify scope:
      - Look for an external issue tracker reference (GitHub, Jira, Linear, …) in branch name, PR title, or commit context. Local file paths do not qualify.
      - Found → use issue as scope.
      - Not found → ask: "Does this relate to an external issue? Provide the number or `none`." Wait for the answer.
        - Number given → use it.
        - `none` → use module → component; omit if neither applies.
   3. Write a commit message per `## Format`.
   4. `git commit`
4. Repeat until `git status --porcelain` is empty.

## Format

```
<type>(<optional scope>): <short imperative description>

[optional body: what and why]

[optional footer]
```

**Types:** `feat` · `fix` · `test` · `style` · `refactor` · `chore` · `docs` · `ci` · `perf`

**Scope examples:** `feat(#42)` (external issue) · `feat(auth)` (module) · `feat(button)` (component)

**Breaking change:** `feat!: ...` + footer `BREAKING CHANGE: <description>`
