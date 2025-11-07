## Stage 6: Git in DevOps Pipelines

### Webhooks (CI Triggers)

A webhook notifies your CI server when events (push/PR) happen. CI pulls the latest commit and runs pipelines.

**High-level flow**

1. Developer pushes to GitHub
2. GitHub sends **webhook** to Jenkins/GitHub Actions
3. Pipeline runs (lint → test → build → deploy)

### Jenkins Integration (Example)

* Install **Git** plugin
* Add **Credentials** (SSH key or PAT)
* Pipeline `Jenkinsfile` example:

```groovy
pipeline {
  agent any
  options { timestamps() }
  triggers { pollSCM('* * * * *') } // or use a GitHub webhook
  stages {
    stage('Checkout') {
      steps {
        checkout scm
      }
    }
    stage('Lint & Test') {
      steps {
        sh 'npm ci'
        sh 'npm run lint'
        sh 'npm test'
      }
    }
    stage('Build') { steps { sh 'npm run build' } }
    stage('Package') { steps { sh 'tar -czf build.tar.gz dist/' } }
  }
  post {
    always { archiveArtifacts artifacts: 'build.tar.gz', fingerprint: true }
  }
}
```

### GitHub Actions (Example)

```yaml
name: ci
on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with: { node-version: 20 }
      - run: npm ci
      - run: npm run lint
      - run: npm test -- --ci
      - run: npm run build
```

### Secrets Management

* **Never** commit secrets; use platform secrets:

  * GitHub: **Repository → Settings → Secrets and variables**
  * Jenkins: **Manage Credentials**
* Prefer **OIDC** or **short-lived tokens** for cloud deploys

### Auth in CI

* Use **deploy keys** (read-only for fetch) or organization-scoped **PAT**
* For private submodules, ensure CI has credentials to fetch

### Monorepos & Submodules

* **Submodules** let you embed another repo at a fixed commit

```bash
git submodule add https://github.com/org/lib-a.git libs/lib-a
```

* Consider **Git sparse-checkout** to limit what CI fetches

```bash
git sparse-checkout init --cone
git sparse-checkout set apps/service-a
```

---
