## Stage 3: Working with Remotes

### Connect Local to Remote

```bash
# Add remote
git remote add origin https://github.com/<user>/demo-repo.git

# Verify
git remote -v
```

### Push & Pull

```bash
# First push creates upstream
git push -u origin main

# Pull latest (fetch + merge)
git pull

# Fetch only (no merge)
git fetch origin
```

### Clone an Existing Repo

```bash
git clone https://github.com/<org>/<repo>.git
cd <repo>
```

### Tracking Branches

```bash
# See upstream tracking
git branch -vv
# Set upstream explicitly
git branch --set-upstream-to=origin/main main
```

### Authentication Options

* **SSH keys** (recommended for dev machines)
* **HTTPS + Personal Access Token (PAT)** (useful in CI)

**Generate SSH Key**

```bash
ssh-keygen -t ed25519 -C "<your_email>"
# Start agent and add key
ssh-agent -s
ssh-add ~/.ssh/id_ed25519
# Copy public key to GitHub
cat ~/.ssh/id_ed25519.pub
```

---
