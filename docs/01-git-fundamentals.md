## Stage 1: Git Fundamentals

### What is Git?

Git is a **distributed version control system** (DVCS). Every clone contains the full history. You can work offline, create branches locally, and sync later.

**Key benefits**

* Complete history on your machine (fast + safe)
* Clear accountability (who changed what, when, and why)
* Easy experimentation via branches

### Git vs. GitHub vs. GitLab

* **Git**: the version control tool (local + CLI)
* **GitHub/GitLab/Bitbucket**: hosted platforms for remote repos, collaboration, CI/CD, permissions, and PRs/MRs

### Core Concepts

* **Repository (repo)**: Project + full history (the `.git/` directory)
* **Commit**: A snapshot with a message
* **Branch**: A movable pointer to a series of commits
* **HEAD**: Your current checkout (usually points to a branch)
* **Remote**: A named connection to a server copy (e.g., `origin`)

### First Repo – From Zero to First Commit

```bash
# 1) Create a folder and initialize
mkdir demo-repo && cd demo-repo
git init

# 2) Add a file
echo "Hello Git" > README.md

# 3) See status and stage
git status
git add README.md

# 4) Commit
git commit -m "chore: initial commit with README"

# 5) View history
git log --oneline
```

### The Staging Area (Index)

```bash
# Stage specific file(s)
git add app.js
# Stage all changes (tracked + untracked)
git add -A
# Unstage a file
git reset HEAD app.js
```

### Inspecting Changes

```bash
# Changes in working directory vs last commit
git diff
# Changes that are staged vs last commit
git diff --cached
# Show a specific commit
git show <commit_sha>
```

### Undoing Safely

```bash
# Amend message or include newly staged changes in last commit
git commit --amend

# Reset modes (DO THIS CAREFULLY):
# soft: keep changes staged
git reset --soft <commit_sha>
# mixed (default): keep changes in working dir, unstage them
git reset <commit_sha>
# hard: discard changes (dangerous)
git reset --hard <commit_sha>

# Life saver: the reflog
git reflog  # find lost commits / branch tips
```

---
