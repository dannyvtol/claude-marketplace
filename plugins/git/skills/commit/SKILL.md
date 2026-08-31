---
name: commit
description: commit changes as conventional commits, sliced by logical concern
---
# Git commit

A **slice** is one logical concern — a feature, fix, or refactor — regardless of how many files it touches. One file may yield multiple slices.

1. Identify scope, once, before slicing. Check sources in order, stop at the first hit:
   1. Branch name.
   2. PR title, if a PR exists for this branch.
   3. Previous commits on this branch, only if it has commits beyond its base (`git log <base>..HEAD`).
   - Hit → external issue reference (GitHub, Jira, Linear, …) is the scope for every commit this session: `<type>(<issue>): ...`. It replaces module/component — never both, never appended after the description.
   - No hit, or the reference is unreliable → ask: "Does this relate to an external issue? Provide the number, or `none`." Wait for the answer.
     - Number given → use it as the scope, as above.
     - `none` → no shared scope; fall back to module/component per slice (step 4.2).
2. Run `git status --porcelain` and `git diff HEAD` to survey all changes.
3. Identify slices. Every hunk must belong to exactly one slice.
4. For each slice:
   1. Stage its changes: `git add -p` for partial files, `git add <file>` for whole files.
   2. No shared scope from step 1 → scope is module → component; omit if neither applies.
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

**Scope examples:** `feat(IT-32998): add optional digidocId to SaveInterestOnlyDigidocJob` (external issue — takes priority) · `feat(auth): ...` (module, no issue) · `feat(button): ...` (component, no issue)

**Breaking change:** `feat!: ...` + footer `BREAKING CHANGE: <description>`
