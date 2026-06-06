---
name: git-worktree
description: 'Manage git worktrees for isolated parallel development environments. Use when user asks to work on multiple features simultaneously, create an isolated environment for a branch, run experiments without affecting the main workspace, or mentions "worktree". Supports: (1) Creating worktrees mapped to Git Flow branches, (2) Listing and navigating active worktrees, (3) Safe cleanup after merge, (4) Parallel feature/hotfix development patterns with oh-my-opencode-slim sub-agents'
---

# Git Worktree Management

## Overview

Git worktrees allow multiple branches to be checked out simultaneously in separate directories — each with its own working state, index, and HEAD. Combined with oh-my-opencode-slim sub-agents, this enables genuine parallel development without context switching or re-cloning.

---

## Core Concept

```
repo/                          ← main worktree (develop or main)
├── .git/
└── src/

/tmp/worktrees/
├── feature-user-auth/         ← worktree for feature/user-auth
├── hotfix-1.1.1/              ← worktree for hotfix/1.1.1
└── release-1.2.0/             ← worktree for release/1.2.0
```

- All worktrees share the same `.git` directory — no full clone overhead
- Each worktree has an independent HEAD, index, and working tree
- Branches in use by a worktree are **locked** and cannot be checked out elsewhere

---

## Worktree Lifecycle

### Create

```bash
# Recommended base path for worktrees
WORKTREE_BASE="/tmp/worktrees"   # or ~/worktrees for persistence

# Create worktree for an existing branch
git worktree add "$WORKTREE_BASE/<branch-slug>" <branch-name>

# Create worktree + new branch simultaneously (Git Flow pattern)
git worktree add -b feature/<name> "$WORKTREE_BASE/feature-<name>" develop
git worktree add -b hotfix/<version> "$WORKTREE_BASE/hotfix-<version>" main
git worktree add -b release/<version> "$WORKTREE_BASE/release-<version>" develop
```

### List

```bash
git worktree list
# Output example:
# /home/user/repo              abc1234 [develop]
# /tmp/worktrees/feature-auth  def5678 [feature/user-auth]
# /tmp/worktrees/hotfix-1.1.1  ghi9012 [hotfix/1.1.1]
```

### Navigate

```bash
# Move into worktree to work
cd "$WORKTREE_BASE/feature-<name>"

# Check which worktrees exist for this repo from anywhere
git -C /path/to/repo worktree list
```

### Cleanup (after merge)

```bash
# 1. Verify branch is merged
git -C /path/to/repo branch --merged develop | grep feature/<name>

# 2. Remove worktree
git worktree remove "$WORKTREE_BASE/feature-<name>"

# 3. If worktree has uncommitted changes, force remove
git worktree remove --force "$WORKTREE_BASE/feature-<name>"

# 4. Prune stale worktree metadata
git worktree prune
```

---

## Git Flow Integration

| Git Flow 단계 | Branch off | Worktree 생성 커맨드 |
|--------------|------------|----------------------|
| Feature 시작  | `develop`  | `git worktree add -b feature/<name> $BASE/feature-<name> develop` |
| Release 시작  | `develop`  | `git worktree add -b release/<ver> $BASE/release-<ver> develop` |
| Hotfix 시작   | `main`     | `git worktree add -b hotfix/<ver> $BASE/hotfix-<ver> main` |

Merge 완료 후에는 반드시 `git worktree remove` → `git worktree prune` 순서로 정리.

---

## Parallel Development with Sub-Agents

oh-my-opencode-slim 환경에서 worktree와 서브에이전트를 조합하는 패턴:

```
Orchestrator
├── Sub-agent A → worktree: feature/user-auth   (독립 컨텍스트)
├── Sub-agent B → worktree: feature/payments    (독립 컨텍스트)
└── Sub-agent C → worktree: hotfix/1.1.1        (독립 컨텍스트)
```

- 각 서브에이전트는 자신의 worktree 경로만 인지 → 컨텍스트 오염 없음
- 한 worktree의 변경이 다른 worktree에 영향 없음
- Orchestrator는 각 서브에이전트 완료 후 메인 브랜치에 순차 merge

---

## Safety Rules

- **NEVER** delete a worktree before verifying the branch is merged or changes are committed
- **NEVER** check out a branch already in use by another worktree (git will reject this)
- **NEVER** run `git worktree remove --force` without explicit user approval and confirmation that no unmerged work exists
- Always run `git worktree prune` after removing worktrees to clean stale metadata
- Worktrees under `/tmp` are lost on reboot — prefer `~/worktrees/<repo>/<branch-slug>` for long-running work
