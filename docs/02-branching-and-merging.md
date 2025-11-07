## Stage 2: Branching & Merging

### Why Branch?

Isolate work (features, fixes, experiments) without breaking `main`.

### Create, Switch, Delete

```bash
# Create branch
git branch feature/login
# Switch to it
git switch feature/login   # modern
# or
git checkout feature/login  # classic

# Create + switch in one step
git switch -c feature/login

# List branches
git branch

# Rename current branch
git branch -m main

# Delete local branch (merged)
git branch -d feature/login
# Force delete (even if unmerged)
git branch -D feature/login
```

### Merge Basics

```bash
# Merge feature into main
git switch main
git merge feature/login
```

* **Fast-forward** merge: when `main` has no new commits since branching, Git just moves the pointer
* **Merge commit**: when both sides progressed; a new commit records the merge

### Solving Conflicts (Pattern)

```bash
# 1) See conflicts in files
# 2) Edit files to resolve markers <<<<<<< ======= >>>>>>>
# 3) Stage resolved files
git add <file>
# 4) Continue the merge
git merge --continue
# If you need to abort
git merge --abort
```

### Common Branching Models

* **Feature Branch Workflow**: create a branch per feature; merge via PR
* **Git Flow**: branches for `main`, `develop`, plus `feature/`, `release/`, `hotfix/`
* **Trunk-Based Development**: short-lived branches frequently merged to `main` with CI gates

**Recommendation for most teams**: Trunk-Based with short-lived feature branches + required PR checks.

---
