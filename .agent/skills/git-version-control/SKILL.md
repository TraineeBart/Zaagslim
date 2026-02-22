---
description: Git Version Control Protocol (Atomic Commits & Merging)
---

# Skill: Git & Version Control

**Goal**: Keep history clean, atomic, and revertible.

## 1. Commit Protocol (Atomic)

*   **Rule**: One logical change per commit.
*   **Format**: Conventional Commits.
    *   `feat(auth): add jwt token support`
    *   `fix(api): handle 404 in user route`
    *   `refactor(db): split models into separate files`
    *   `docs: update readme`
    *   `chore: update dependencies`

### ❌ Bad Commit Messages
*   "Fix"
*   "Update code"
*   "WIP"

## 2. Branching Strategy (Solo Developer)

We use a simplified flow because there is no PR review bottleneck.

1.  **Feature Branch**: `git checkout -b feat/my-feature`
2.  **Work**: Commit atomic changes.
3.  **Verify**: Run tests locally.
4.  **Merge**:
    ```bash
    git checkout main
    git merge feat/my-feature
    git branch -d feat/my-feature
    ```
    *   *Note*: Fast-forward is preferred if no conflicts.

## 3. Emergency Revert

If `main` is broken:
```bash
git checkout main
git revert HEAD
# Fix the issue in a new branch
```
