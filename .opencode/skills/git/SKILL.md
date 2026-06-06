---
name: git
description: 'Git commit and branch management following Git Flow strategy and Conventional Commits specification. Use when user asks to commit changes, create/merge branches, start a feature/release/hotfix, stage files, or mentions "/commit". Supports: (1) Auto-detecting type and scope from changes, (2) Generating conventional commit messages from diff, (3) Git Flow branch lifecycle (feature/release/hotfix), (4) Intelligent file staging, (5) Repository remote management'
license: MIT
---

# Git Commit & Git Flow Branch Management

## Overview

Create standardized, semantic git commits using the Conventional Commits specification, and manage branches following the Git Flow strategy. Analyze the actual diff to determine appropriate type, scope, and message.

---

## Git Flow Branch Strategy

### Branch Structure

```
main          ─────●─────────────────────●─────────────────●──▶
                   │ (tag: v1.0)          │ (tag: v1.1)     │ (tag: v2.0)
develop       ─────●──────●──────●───────●──────────────────●──▶
                          │      │                           │
feature/*          ────●──┘      │                           │
release/*                  ────●─┘                           │
hotfix/*                                               ────●─┘
```

### Branch Naming Rules

| Branch       | Pattern                        | Example                     |
| ------------ | ------------------------------ | --------------------------- |
| `main`       | permanent                      | `main`                      |
| `develop`    | permanent                      | `develop`                   |
| `feature/*`  | `feature/<issue-or-name>`      | `feature/user-auth`         |
| `release/*`  | `release/<version>`            | `release/1.2.0`             |
| `hotfix/*`   | `hotfix/<version-or-name>`     | `hotfix/1.1.1`              |

---

## Git Flow Workflow

### Feature Development

```bash
# Start feature (branch off develop)
git checkout develop
git pull origin develop
git checkout -b feature/<name>

# ... commit work ...

# Finish feature (merge back to develop)
git checkout develop
git merge --no-ff feature/<name> -m "feat(<scope>): merge feature/<name>"
git branch -d feature/<name>
git push origin develop
```

### Release

```bash
# Start release (branch off develop)
git checkout develop
git checkout -b release/<version>

# Only bug fixes and release prep commits allowed here
# bump version, update changelog...

# Finish release (merge to main AND develop)
git checkout main
git merge --no-ff release/<version> -m "chore(release): v<version>"
git tag -a v<version> -m "v<version>"

git checkout develop
git merge --no-ff release/<version> -m "chore(release): merge release/<version> back to develop"

git branch -d release/<version>
git push origin main develop --tags
```

### Hotfix

```bash
# Start hotfix (branch off main)
git checkout main
git checkout -b hotfix/<version>

# Fix the bug, commit with fix type

# Finish hotfix (merge to main AND develop)
git checkout main
git merge --no-ff hotfix/<version> -m "fix: merge hotfix/<version>"
git tag -a v<version> -m "v<version>"

git checkout develop
git merge --no-ff hotfix/<version> -m "fix: merge hotfix/<version> into develop"

git branch -d hotfix/<version>
git push origin main develop --tags
```

### Merge Policy

- Always use `--no-ff` (no fast-forward) when merging feature/release/hotfix branches
- This preserves branch topology in the history graph
- Direct commits to `main` are **forbidden** — only merges from `release/*` or `hotfix/*`
- Direct commits to `develop` should be avoided — prefer feature branches

---

## Conventional Commit Format

```
<type>[optional scope]: <description>

[optional body]

[optional footer(s)]
```

---

## Commit Types

| Type       | Purpose                        |
| ---------- | ------------------------------ |
| `feat`     | New feature                    |
| `fix`      | Bug fix                        |
| `docs`     | Documentation only             |
| `style`    | Formatting/style (no logic)    |
| `refactor` | Code refactor (no feature/fix) |
| `perf`     | Performance improvement        |
| `test`     | Add/update tests               |
| `build`    | Build system/dependencies      |
| `ci`       | CI/config changes              |
| `chore`    | Maintenance/misc               |
| `revert`   | Revert commit                  |

---

## Breaking Changes

```
# Exclamation mark after type/scope
feat!: remove deprecated endpoint

# BREAKING CHANGE footer
feat: allow config to extend other configs

BREAKING CHANGE: `extends` key behavior changed
```

---

## Commit Workflow

### 1. Analyze Diff

```bash
# If files are staged, use staged diff
git diff --staged

# If nothing staged, use working tree diff
git diff

# Also check status
git status --porcelain
```

### 2. Stage Files (if needed)

```bash
# Stage specific files
git add path/to/file1 path/to/file2

# Stage by pattern
git add *.test.*
git add src/components/*

# Interactive staging
git add -p
```

**Never commit secrets** (.env, credentials.json, private keys).

### 3. Generate Commit Message

Analyze the diff to determine:

- **Type**: What kind of change is this?
- **Scope**: What area/module is affected?
- **Description**: One-line summary of what changed (present tense, imperative mood, <72 chars)

### 4. Execute Commit

```bash
# Single line
git commit -m "<type>[scope]: <description>"

# Multi-line with body/footer
git commit -m "$(cat <<'EOF'
<type>[scope]: <description>

<optional body>

<optional footer>
EOF
)"
```

---

## Best Practices

- One logical change per commit
- Present tense: "add" not "added"
- Imperative mood: "fix bug" not "fixes bug"
- Reference issues: `Closes #123`, `Refs #456`
- Keep description under 72 characters

---

## Git Safety Protocol

- Before committing, inspect `git status`, relevant `git diff`, and recent commit style.
- **NEVER** update git config
- **NEVER** run destructive commands (`--force`, hard reset) without explicit request
- **NEVER** skip hooks (`--no-verify`) unless user asks
- **NEVER** force push to `main`/`master` or `develop`
- **NEVER** commit directly to `main` — only merge via `release/*` or `hotfix/*`
- If commit fails due to hooks, fix and create **NEW** commit (don't amend)
