---
name: git-commit
description: Add meaning to commit messages
---
# Git commit

A **slice** is one logical concern — a feature, fix, or refactor — regardless of how many files it touches. One file may yield multiple slices.

1. Run `git status --porcelain` and `git diff -p` to survey all changes.
2. Identify slices. Every hunk must belong to exactly one slice.
3. For each slice:
   1. Stage its hunks: `git add -p` for partial files, `git add <file>` for whole files.
   2. Write a commit message per `## Format` and `## Rules`.
   3. `git commit`
4. Repeat until `git status --porcelain` shows no unstaged changes.

## Format

```
<type>(<optional scope>): <short imperative description>

[optional body explaining *what* and *why*]

[optional footer]
```

## Types

- `feat`: New feature
- `fix`: Bug fix
- `test`: Adding/fixing tests
- `style`: Formatting, whitespace (no logic change)
- `refactor`: Reorganizing codebase only
- `chore`: Build, tooling, deps
- `docs`: Documentation only
- `ci`: CI/CD changes

## Rules

- Type + description: **required**
- Scope: optional, links issue, in parentheses → `feat(#1): ...`
- Breaking change: add `!` before `:` → `feat!: ...`
- Breaking change footer: `BREAKING CHANGE: <description>`
- Body/footers separated from description by one blank line
