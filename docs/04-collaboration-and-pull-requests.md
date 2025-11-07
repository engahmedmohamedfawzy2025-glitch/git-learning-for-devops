## Stage 4: Collaboration & Pull Requests

### Fork vs Clone

* **Clone**: copy a repo you can push to (if you have rights)
* **Fork**: your own server-side copy under your account (open-source flow)

### Pull Request (PR) Flow (Typical)

1. Branch from `main`: `feature/awesome`
2. Commit small, descriptive changes
3. Push and open a PR with a clear title + description
4. CI runs; reviewers comment
5. Address feedback (extra commits or squash)
6. Merge (merge commit / squash / rebase)
7. Delete the branch

**Good PR Description Template**

```
Title: feat(login): add OAuth2 login with Google

Summary:
- Introduces OAuth2 login using Google
- Adds /auth routes and JWT issuance
- Updates user model with oauth_provider

Testing:
- Unit tests for auth controller
- Manual test with Google test account

Risk/Impact:
- New env vars required: GOOGLE_CLIENT_ID, GOOGLE_CLIENT_SECRET
```

### Code Review Guidelines (for Managers & DevOps)

* Keep PRs small and focused (prefer < 300 lines)
* Require CI green status before merge
* Enforce **branch protection rules** on `main` (reviews, status checks)
* Automate lint/tests to block low-quality changes

---
