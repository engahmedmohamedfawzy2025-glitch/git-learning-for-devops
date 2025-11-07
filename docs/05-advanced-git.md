## Stage 5: Advanced Git

### Rebase vs Merge

* **Merge** preserves true history with merge commits
* **Rebase** rewrites your branch to appear as if based on the latest `main` → cleaner, linear history

```bash
# Rebase your feature onto latest main
git switch feature/x
git fetch origin
git rebase origin/main
# If conflicts: resolve + continue
git rebase --continue
# If it goes wrong
git rebase --abort
```

**Rule of thumb**: Rebase **only your local / unshared** branches. Avoid rebasing public history.

### Squash Commits

```bash
# Interactive rebase to squash commits
git rebase -i HEAD~5
# mark older commits as 's' or 'fixup'
```

### Cherry-Pick

Bring a specific commit into your branch.

```bash
git switch release/1.2.0
git cherry-pick <commit_sha>
```

### Stash – Shelve WIP Temporarily

```bash
# Stash changes
git stash push -m "WIP: experimenting with parser"
# List stashes
git stash list
# Apply latest stash (keep it in stash)
git stash apply
# Pop (apply + drop)
git stash pop
```

### Tags & Releases

```bash
# Lightweight tag
git tag v1.0.0
# Annotated tag (recommended)
git tag -a v1.0.0 -m "Release 1.0.0"
# Push tags
git push --tags
```

### .gitignore Essentials

* Ignore build artifacts, secrets, local env files
* Keep `.env.example` checked in for required variables

See [Sample .gitignore](#appendix-sample-gitignore).

### Git Hooks (Automation at the Edges)

* **Client hooks** (in `.git/hooks/`): e.g., `pre-commit` → run linters/tests before committing
* **Server hooks**: on the remote side (e.g., enforce messages)

Example `pre-commit` (make executable):

```bash
#!/usr/bin/env bash
set -e
npm run lint
npm test
```

### Signing Commits (GPG)

```bash
# Generate key (GPG)
gpg --full-generate-key
# List keys and copy KEYID
gpg --list-secret-keys --keyid-format=long
# Configure Git
git config --global user.signingkey <KEYID>
git config --global commit.gpgsign true
```

### Safety Tools

* `git reflog` to recover lost work
* `git restore` for files; `git reset` for index/commits
* Use `--force-with-lease` instead of `--force`

---
