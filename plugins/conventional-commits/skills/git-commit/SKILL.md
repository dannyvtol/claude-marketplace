---
name: git-commit
description: commit changes as conventional commits, sliced by logical concern
---
# Git commit

A **slice** is one logical concern — a feature, fix, or refactor — regardless of how many files it touches. One file may yield multiple slices.

1. Run `git status --porcelain` and `git diff HEAD` to survey all changes.
2. Identify slices. Every hunk must belong to exactly one slice.
3. For each slice:
   1. Stage its changes: `git add -p` for partial files, `git add <file>` for whole files.
   2. Identify scope (priority: issue # → module → component; omit if none applies).
   3. Write a commit message per `## Format` and `## Rules`.
   4. `git commit`
4. Repeat until `git status --porcelain` is empty.

## Format

```
<type>(<optional scope>): <short imperative description>

[optional body explaining *what* and *why*]

[optional footer]
```

## Types

- `feat`: New feature
- `fix`: Bug fix
- `test`: Tests
- `style`: Formatting, no logic change
- `refactor`: Restructuring only
- `chore`: Build, tooling, deps
- `docs`: Documentation
- `ci`: CI/CD

## Rules

- Type + description: **required**
- Scope: optional; `feat(#42): ...` (issue), `feat(auth): ...` (module), `feat(button): ...` (component)
- Breaking change: add `!` before `:` → `feat!: ...`
- Breaking change footer: `BREAKING CHANGE: <description>`
- Body/footers separated from description by one blank line
