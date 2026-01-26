---
title: 'Understanding GitHub Actions Workflow Files (YAML Explained in Detail)'
description: 'A practical and beginner-friendly guide to GitHub Actions workflow YAML files, explaining triggers, jobs, steps, secrets, and real-world CI/CD use cases.'
pubDate: 'May 14 2023'
heroImage: '../../assets/blog-placeholder-2.jpg'
readTime: '7 min'
tags: ['github', 'github-actions', 'ci-cd', 'devops', 'yaml']
---

### Understanding GitHub Actions Workflow Files (YAML Explained in Detail)

### What Is a GitHub Actions Workflow?

A workflow is an automated process defined in a YAML file that runs when a specific event happens in your repository.

Common events include:

- Pushing code to a branch
- Opening or merging a pull request
- Manually triggering a workflow
- Running on a schedule (cron jobs)

Workflow files live inside this directory:

```
.github/workflows/
```

Each file represents one workflow.

### Basic Structure of a Workflow File

A minimal GitHub Actions workflow looks like this:

```yaml
name: Example Workflow

on:
  push:
    branches:
      - main

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v3
```

## Let’s break it down.

### The name Field

```yaml
name: Example Workflow
```

This is simply the **display** name of the workflow.
You’ll see it in the Actions tab on GitHub.

It has no technical impact — it’s just for readability.

---

### The on Section (Triggers)

The on key defines **_when the workflow should run._**

Example: Run on push to a branch

```yaml
on:
push:
branches: - main
```

This means:

**_Run this workflow whenever code is pushed to the main branch._**

Other common triggers:

```yaml
on:
pull_request:
workflow_dispatch:
```

- pull_request → runs when PRs are opened or updated

- workflow_dispatch → allows manual execution from GitHub UI

### The jobs Section

A workflow is made up of one or more jobs.

```yaml
jobs:
build:
runs-on: ubuntu-latest
```

Here:

- build is the job name

- runs-on specifies the virtual machine environment

Common runners:

- ubuntu-latest

- windows-latest

- macos-latest

Each job runs in a _fresh, isolated environment._

### Steps: The Heart of the Workflow

Inside a job, you define steps — individual tasks executed in order.

```yaml
steps:
  - name: Checkout code
    uses: actions/checkout@v3
```

Each step can:

- Run a command

- Use a pre-built GitHub Action

- Execute shell scripts

Steps run sequentially, top to bottom.

### uses vs run

Using an existing action

```yaml
- name: Checkout code
  uses: actions/checkout@v3
```

This pulls a reusable action from GitHub Marketplace.

Running shell commands

```yaml
- name: Install dependencies
  run: pnpm install
```

By default:

- Linux/macOS → Bash

- Windows → PowerShell

You can run any command your environment supports.

---

## Environment Variables and Secrets

### Using GitHub Secrets

Secrets are stored securely in:

```
Repo → Settings → Secrets and variables → Actions
```

Usage in workflow:

```yaml
env:
API_KEY: ${{ secrets.API_KEY }}
```

Or inside a step:

```yaml
run: echo ${{ secrets.API_KEY }}
```

Secrets are:

- Encrypted

- Hidden in logs

- Essential for deployment workflows

### A Real-World Example: Deployment Workflow

```yaml
name: Xsite Staging Deployment

on:
  push:
    branches:
      - v2

jobs:
  deploy:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout Code
        uses: actions/checkout@v3

      - name: Connect to VM and Deployment
        uses: appleboy/ssh-action@v1.2.0
        with:
          host: ${{ secrets.VM_HOST}}
          username: ${{ secrets.VM_USERNAME}}
          password: ${{ secrets.VM_PASSWORD}}
          port: ${{secrets.VM_PORT}}
          script: |
            echo "Starting Deployment...milanpraz"
            cd /var/www/production/xsite-builder

            echo "Pulling latest changes from v2 branch....milanpraz"
            git fetch origin
            git checkout v2
            git pull origin v2

            echo "Installing dependencies...milanpraz"
            pnpm install 

            echo "Building the project...milanpraz"
            pnpm build 

            echo "Restarting PM2 process...milanpraz"
            pm2 restart xsite-builder

            echo "Deployment completed successfully!milanpraz"
```
