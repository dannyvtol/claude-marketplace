---
name: commit
description: commit changes as conventional commits, sliced by logical concern
---
# Git commit

A **slice** is one logical concern — a feature, fix, or refactor — regardless of how many files it touches. One file may yield multiple slices.

1. **Lock the scope** once, before slicing. Run `git branch --show-current`, then check in order, stop at the first hit:
   1. **Branch name** — extract the issue key: `feat/2-scaffold` → `#2`; `fix/PROJ-123-foo` → `PROJ-123`. A bare number is a GitHub issue (`#N`); an alphanumeric key is a tracker ID.
   2. **PR title** — `gh pr view --json title`, if a PR exists for this branch.
   3. **Prior commits** — `git log <base>..HEAD`, only when commits exist beyond the base.
   - **Hit** → the issue key is the **locked scope** for every commit this session. Format: `<type>(<issue>): ...`. The issue key is the complete scope; drop module/component.
   - **No hit** → ask: "Does this relate to an external issue? Provide the number, or `none`." Wait for the answer.
     - Number given → lock it as scope, as above.
     - `none` → no locked scope; derive scope per slice in step 4.2.
2. Run `git status --porcelain` and `git diff HEAD` to survey all changes.
3. Identify slices. Every hunk must belong to exactly one slice.
4. For each slice:
   1. Stage its changes: `git add -p` for partial files, `git add <file>` for whole files.
   2. Scope: use the locked scope from step 1; if none, use module → component; omit if neither applies.
   3. Write a commit message per `## Format`.
   4. `git commit`
5. Repeat until `git status --porcelain` is empty.

## Format

```
<type>(<optional scope>): <short imperative description>

[optional body: what and why]

[optional footer]
```

**Types:** `feat` · `fix` · `test` · `style` · `refactor` · `chore` · `docs` · `ci` · `perf`

**Scope examples:** `feat(#2): ...` (locked scope, GitHub) · `feat(IT-32998): add optional digidocId to SaveInterestOnlyDigidocJob` (locked scope, Jira) · `feat(auth): ...` (module) · `feat(button): ...` (component)

**Breaking change:** `feat!: ...` + footer `BREAKING CHANGE: <description>`
