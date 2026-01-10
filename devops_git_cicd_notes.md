# DevOps Learning Notes: Git & CI/CD with GitHub Actions

## Table of Contents
1. [Git Basics](#git-basics)
2. [Git Configuration](#git-configuration)
3. [Working with Repositories](#working-with-repositories)
4. [Branching and Merging](#branching-and-merging)
5. [Remote Repositories](#remote-repositories)
6. [Git Cheat Sheet](#git-cheat-sheet)
7. [CI/CD with GitHub Actions](#cicd-with-github-actions)
8. [Your First Pipeline](#your-first-pipeline)
9. [Advanced Pipeline Example](#advanced-pipeline-example)
10. [Understanding GitHub Actions Tab](#understanding-github-actions-tab)

---

## Git Basics

### What is Git?
Git is a distributed version control system that tracks changes in your code over time. It allows multiple developers to work on the same project without conflicts and maintains a complete history of all changes.

### Checking Git Version
```bash
git --version
```
This command shows which version of Git is installed on your system.

---

## Git Configuration

### Setting Up Your Identity
Before you start using Git, you need to configure your username and email. These details will be attached to your commits.

```bash
git config --global user.name "Adrian"
git config --global user.email "contact@email.com"
```

**What does `--global` mean?**
- `--global`: Applies to all repositories on your computer
- Without `--global`: Applies only to the current repository

### Setting Default Branch Name
```bash
git config --global init.defaultBranch main
```
This sets "main" as the default branch name for new repositories (previously it was "master").

---

## Working with Repositories

### Initializing a Repository
```bash
git init
```
Creates a new Git repository in your current directory. This creates a hidden `.git` folder that tracks all changes.

### Checking Repository Status
```bash
git status
```
Shows the current state of your repository:
- Which files have been modified
- Which files are staged for commit
- Which branch you're on

### Adding Files to Staging Area
```bash
# Add a specific file
git add readme.md

# Add all files
git add .
```

**What is the staging area?**
Think of it as a preparation area where you choose which changes to include in your next commit.

### Committing Changes
```bash
git commit -m 'message'
git commit -m 'add all files'
```
A commit is a snapshot of your project at a specific point in time. The `-m` flag lets you add a descriptive message.

**Best practices for commit messages:**
- Be clear and descriptive
- Use present tense ("add feature" not "added feature")
- Keep it concise but meaningful

### Viewing Commit History
```bash
git log
```
Shows a list of all commits with their IDs, authors, dates, and messages.

---

## Branching and Merging

### Understanding Branches
Branches allow you to work on different features or experiments without affecting the main codebase.

### Navigating Between Commits and Branches
```bash
# Go to a specific commit
git checkout f123142f231b123123d232

# Return to main branch
git checkout main

# Force checkout (discards local changes)
git checkout -f main
```

**Warning:** `git checkout -f` will discard any uncommitted changes!

### Renaming Branches
```bash
git branch -M main
```
Renames the current branch to "main". The `-M` flag forces the rename even if a branch with that name exists.

### Creating and Switching Branches
```bash
# Create a new branch
git branch branch-name

# Switch to that branch
git checkout branch-name

# Create and switch in one command
git checkout -b feature-branch

# Create a branch from another branch
git branch new-branch-name source-branch
```

### Working with Feature Branches
A typical workflow:
1. Create a feature branch from main
2. Make changes in the feature branch
3. Commit your changes
4. Push to remote repository
5. Create a pull request to merge into main

---

## Remote Repositories

### Adding Remote Repositories
```bash
# Add a remote called 'origin'
git remote add origin https://github.com/remote/repo.git

# You can add multiple remotes
git remote add something_else https://github.com/remote/new.git
```

**What is 'origin'?**
It's just a conventional name for your primary remote repository. You can name it anything.

### Pushing Changes
```bash
# First push (sets upstream)
git push -u origin main

# Same as above
git push --set-upstream origin feature-branch

# Subsequent pushes
git push
```

**What does `-u` do?**
It sets the upstream branch, creating a tracking relationship. After this, you can simply use `git push` without specifying the remote and branch.

### Pulling Changes
```bash
git pull
```
Fetches changes from the remote repository and merges them into your current branch.

---

## Git Cheat Sheet

### Setup and Configuration
| Command | Description |
|---------|-------------|
| `git --version` | Check Git version |
| `git config --global user.name "Name"` | Set your name |
| `git config --global user.email "email@example.com"` | Set your email |
| `git config --list` | View all configurations |
| `git config --global init.defaultBranch main` | Set default branch name |

### Repository Basics
| Command | Description |
|---------|-------------|
| `git init` | Initialize a new repository |
| `git clone <url>` | Clone a remote repository |
| `git status` | Check repository status |
| `git add <file>` | Stage a specific file |
| `git add .` | Stage all changes |
| `git commit -m "message"` | Commit staged changes |
| `git commit -am "message"` | Stage and commit in one step |
| `git log` | View commit history |
| `git log --oneline` | Compact commit history |
| `git log --graph` | Visual commit graph |

### Branching
| Command | Description |
|---------|-------------|
| `git branch` | List all branches |
| `git branch <name>` | Create a new branch |
| `git branch -d <name>` | Delete a branch |
| `git branch -D <name>` | Force delete a branch |
| `git branch -M <name>` | Rename current branch |
| `git checkout <branch>` | Switch to a branch |
| `git checkout -b <name>` | Create and switch to new branch |
| `git switch <branch>` | Modern way to switch branches |
| `git switch -c <name>` | Create and switch (modern) |

### Remote Repositories
| Command | Description |
|---------|-------------|
| `git remote` | List remote repositories |
| `git remote -v` | List remotes with URLs |
| `git remote add <name> <url>` | Add a remote repository |
| `git remote remove <name>` | Remove a remote |
| `git push <remote> <branch>` | Push to remote |
| `git push -u <remote> <branch>` | Push and set upstream |
| `git pull` | Fetch and merge changes |
| `git fetch` | Fetch changes without merging |

### Undoing Changes
| Command | Description |
|---------|-------------|
| `git checkout -- <file>` | Discard changes in file |
| `git checkout -f` | Force discard all changes |
| `git reset <file>` | Unstage a file |
| `git reset --soft HEAD~1` | Undo last commit, keep changes |
| `git reset --hard HEAD~1` | Undo last commit, discard changes |
| `git revert <commit>` | Create new commit that undoes changes |

### Viewing Changes
| Command | Description |
|---------|-------------|
| `git diff` | Show unstaged changes |
| `git diff --staged` | Show staged changes |
| `git diff <branch1> <branch2>` | Compare branches |
| `git show <commit>` | Show specific commit |

### Stashing
| Command | Description |
|---------|-------------|
| `git stash` | Save changes temporarily |
| `git stash list` | List all stashes |
| `git stash pop` | Apply and remove latest stash |
| `git stash apply` | Apply stash without removing |
| `git stash drop` | Delete a stash |

### Merging
| Command | Description |
|---------|-------------|
| `git merge <branch>` | Merge branch into current |
| `git merge --abort` | Abort a merge |
| `git rebase <branch>` | Rebase current branch |

---

## CI/CD with GitHub Actions

### What is CI/CD?

**Continuous Integration (CI):**
Automatically building and testing code every time changes are pushed to the repository. This helps catch bugs early.

**Continuous Deployment/Delivery (CD):**
Automatically deploying your application to production or staging environments after passing tests.

### GitHub Actions Overview

GitHub Actions is GitHub's built-in CI/CD platform that automates workflows based on events in your repository.

### Key Concepts

**Workflow:** An automated process defined in a YAML file
**Event:** Something that triggers a workflow (push, pull request, etc.)
**Job:** A set of steps that execute on the same runner
**Step:** An individual task within a job
**Runner:** A server that runs your workflows (GitHub-hosted or self-hosted)

### Essential YAML Keywords

| Keyword | Description |
|---------|-------------|
| `name` | Name of the workflow |
| `on` | Events that trigger the workflow |
| `jobs` | Contains all the jobs in the workflow |
| `steps` | Individual tasks within a job |
| `run` | Executes command-line commands |
| `uses` | Uses a pre-built action |
| `with` | Provides input parameters to an action |
| `env` | Sets environment variables |
| `needs` | Specifies job dependencies |

---

## Your First Pipeline

You created a simple Node.js project with a CI pipeline. Let's break down what each part does.

### Project Structure
```
devops/
├── .github/
│   └── workflows/
│       └── pipeline.yaml
├── index.js
├── test.js
└── package.json
```

### Your Files Explained

**index.js** - Main application file
```javascript
console.log("index.js");
```

**test.js** - Test file
```javascript
console.log("starting test...");
setTimeout(() => {
  console.log("running test...");
}, 3000);
console.log("finish test");
```

**package.json** - Node.js project configuration
```json
{
  "name": "devops",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "run": "node index.js",
    "test": "node test.js"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "type": "commonjs"
}
```

**Scripts section explained:**
- `npm run` → executes `node index.js`
- `npm test` → executes `node test.js`

### Your Pipeline Breakdown

```yaml
name: CI PIPELINE
```
Names your workflow "CI PIPELINE" (visible in GitHub Actions tab)

```yaml
on:
  push:
    branches: [main]
```
Triggers the workflow whenever code is pushed to the `main` branch

```yaml
jobs:
  build:
    runs-on: ubuntu-latest
```
Creates a job named "build" that runs on the latest Ubuntu virtual machine

```yaml
    steps:
      - name: Checkout code
        uses: actions/checkout@v5
```
**Step 1:** Downloads your repository code to the runner

```yaml
      - name: Set up Node.js
        uses: actions/setup-node@v3
        with:
          node-version: 16
```
**Step 2:** Installs Node.js version 16 on the runner

```yaml
      - name: Install dependencies
        run: npm install
```
**Step 3:** Installs all dependencies listed in package.json

```yaml
      - name: Run tests
        run: npm test
```
**Step 4:** Runs your test script

---

## Advanced Pipeline Example

Here's a more comprehensive pipeline with multiple jobs, environments, and deployment simulation:

```yaml
name: Advanced CI/CD Pipeline

on:
  push:
    branches: [main, develop]
  pull_request:
    branches: [main]

env:
  NODE_VERSION: '18'
  APP_NAME: 'devops-demo'

jobs:
  # Job 1: Code Quality Checks
  lint:
    name: Code Quality Check
    runs-on: ubuntu-latest
    
    steps:
      - name: Checkout code
        uses: actions/checkout@v5
      
      - name: Setup Node.js
        uses: actions/setup-node@v3
        with:
          node-version: ${{ env.NODE_VERSION }}
          cache: 'npm'
      
      - name: Install dependencies
        run: npm ci
      
      - name: Run linter
        run: npm run lint --if-present
        continue-on-error: true

  # Job 2: Run Tests
  test:
    name: Run Tests
    runs-on: ubuntu-latest
    needs: lint
    
    strategy:
      matrix:
        node-version: [16, 18, 20]
    
    steps:
      - name: Checkout code
        uses: actions/checkout@v5
      
      - name: Setup Node.js ${{ matrix.node-version }}
        uses: actions/setup-node@v3
        with:
          node-version: ${{ matrix.node-version }}
      
      - name: Install dependencies
        run: npm ci
      
      - name: Run tests
        run: npm test
      
      - name: Generate test report
        run: echo "Tests passed on Node.js ${{ matrix.node-version }}"

  # Job 3: Build Application
  build:
    name: Build Application
    runs-on: ubuntu-latest
    needs: test
    
    steps:
      - name: Checkout code
        uses: actions/checkout@v5
      
      - name: Setup Node.js
        uses: actions/setup-node@v3
        with:
          node-version: ${{ env.NODE_VERSION }}
      
      - name: Install dependencies
        run: npm ci
      
      - name: Build application
        run: npm run build --if-present
      
      - name: Create artifact
        run: |
          mkdir -p artifacts
          cp -r . artifacts/${{ env.APP_NAME }}
      
      - name: Upload build artifacts
        uses: actions/upload-artifact@v3
        with:
          name: build-artifacts
          path: artifacts/
          retention-days: 5

  # Job 4: Security Scan
  security:
    name: Security Scan
    runs-on: ubuntu-latest
    needs: build
    
    steps:
      - name: Checkout code
        uses: actions/checkout@v5
      
      - name: Run security audit
        run: npm audit --audit-level=moderate
        continue-on-error: true
      
      - name: Check for vulnerabilities
        run: echo "Security scan completed"

  # Job 5: Deploy to Staging
  deploy-staging:
    name: Deploy to Staging
    runs-on: ubuntu-latest
    needs: [build, security]
    if: github.ref == 'refs/heads/develop'
    environment:
      name: staging
      url: https://staging.example.com
    
    steps:
      - name: Download artifacts
        uses: actions/download-artifact@v3
        with:
          name: build-artifacts
      
      - name: Deploy to staging
        run: |
          echo "Deploying to staging environment..."
          echo "Application: ${{ env.APP_NAME }}"
          echo "Version: ${{ github.sha }}"
          # Add your deployment commands here
      
      - name: Verify deployment
        run: echo "Deployment verification completed"

  # Job 6: Deploy to Production
  deploy-production:
    name: Deploy to Production
    runs-on: ubuntu-latest
    needs: [build, security]
    if: github.ref == 'refs/heads/main'
    environment:
      name: production
      url: https://production.example.com
    
    steps:
      - name: Download artifacts
        uses: actions/download-artifact@v3
        with:
          name: build-artifacts
      
      - name: Deploy to production
        run: |
          echo "Deploying to production environment..."
          echo "Application: ${{ env.APP_NAME }}"
          echo "Version: ${{ github.sha }}"
          # Add your deployment commands here
      
      - name: Notify team
        run: echo "Production deployment completed successfully!"

  # Job 7: Cleanup
  cleanup:
    name: Cleanup
    runs-on: ubuntu-latest
    needs: [deploy-staging, deploy-production]
    if: always()
    
    steps:
      - name: Cleanup resources
        run: echo "Cleaning up temporary resources..."
```

### Advanced Pipeline Features Explained

**Multiple Triggers:**
```yaml
on:
  push:
    branches: [main, develop]
  pull_request:
    branches: [main]
```
Runs on pushes to main/develop and on pull requests to main.

**Environment Variables:**
```yaml
env:
  NODE_VERSION: '18'
  APP_NAME: 'devops-demo'
```
Define variables once, use throughout the workflow with `${{ env.VARIABLE_NAME }}`.

**Job Dependencies:**
```yaml
needs: lint
```
Ensures jobs run in sequence. This job waits for the "lint" job to complete.

**Matrix Strategy:**
```yaml
strategy:
  matrix:
    node-version: [16, 18, 20]
```
Runs the same job multiple times with different configurations. Tests on Node 16, 18, and 20.

**Conditional Execution:**
```yaml
if: github.ref == 'refs/heads/main'
```
Only runs this job when pushing to the main branch.

**Artifacts:**
```yaml
- uses: actions/upload-artifact@v3
  with:
    name: build-artifacts
    path: artifacts/
```
Saves files between jobs. Later jobs can download these artifacts.

**Environments:**
```yaml
environment:
  name: production
  url: https://production.example.com
```
Defines deployment environments with protection rules and URLs.

---

## Understanding GitHub Actions Tab

After you push your pipeline file to GitHub, here's what to expect in the **Actions** tab:

### Accessing the Actions Tab
1. Go to your repository on GitHub
2. Click on the "Actions" tab (between "Pull requests" and "Projects")

### What You'll See

**Workflows Section (Left Sidebar):**
- Lists all your workflow files
- Shows workflow names (e.g., "CI PIPELINE", "Advanced CI/CD Pipeline")
- Click on a workflow to filter runs for that specific workflow

**Workflow Runs (Main Area):**
- **Status Icons:**
  - ✅ Green checkmark = Success
  - ❌ Red X = Failed
  - 🟡 Yellow dot = In progress
  - ⚫ Gray dot = Cancelled or skipped

- **Run Information:**
  - Commit message that triggered the run
  - Branch name
  - Who triggered it (your username)
  - When it was triggered
  - How long it took to complete

### Viewing a Specific Run

Click on any workflow run to see:

**Summary Page:**
- Overall status
- Jobs visualization (shows all jobs and their status)
- Artifacts (if any were created)
- Annotations (errors or warnings)

**Jobs Details:**
Click on a job name (e.g., "build") to see:
- Each step with its status
- Expandable logs for each step
- Execution time for each step
- Any error messages

**Example of what you'll see:**
```
✅ Checkout code (1s)
✅ Set up Node.js (3s)
✅ Install dependencies (15s)
❌ Run tests (2s)
   Error: Test failed on line 5
   Expected: true
   Received: false
```

### Re-running Workflows

- Click "Re-run all jobs" to run the workflow again
- Useful when a job fails due to temporary issues

### Filtering and Search

- Filter by event (push, pull_request, schedule)
- Filter by branch
- Filter by status (success, failure, in progress)
- Search by commit message or SHA

### Workflow Insights

Click on a workflow name, then "View all runs" to see:
- Success rate over time
- Average run duration
- Most common failures
- Historical trends

### Setting Up Notifications

Go to repository Settings → Notifications to configure:
- Email notifications for workflow failures
- GitHub notifications
- Integration with Slack or other tools

### Protection Rules

For production deployments, you can set up:
- Required reviewers before deployment
- Wait timers
- Environment-specific secrets

### Debugging Failed Runs

When a workflow fails:
1. Click on the failed run
2. Click on the failed job
3. Expand the failed step
4. Read the error logs
5. Look for:
   - Syntax errors in your code
   - Missing dependencies
   - Configuration issues
   - Permission problems

### Common Issues You Might See

**"npm: command not found"**
- Node.js wasn't set up properly
- Check your setup-node step

**"Permission denied"**
- Missing repository permissions
- Check your workflow permissions in settings

**"Workflow file is not valid"**
- YAML syntax error
- Use a YAML validator to check your file

### Best Practices

1. **Name your steps clearly** - Makes debugging easier
2. **Use caching** - Speeds up workflow runs
3. **Set timeouts** - Prevent workflows from running forever
4. **Use secrets for sensitive data** - Never hardcode passwords or API keys
5. **Monitor your workflow runs** - Check regularly for failures
6. **Keep workflows focused** - Don't try to do too much in one workflow

### Example: What Success Looks Like

After pushing your code, within minutes you'll see:

```
CI PIPELINE #42
✅ Completed in 1m 23s

Jobs:
  ✅ build (1m 23s)
    ✅ Checkout code (2s)
    ✅ Set up Node.js (5s)
    ✅ Install dependencies (45s)
    ✅ Run tests (31s)
```

This confirms:
- Your code was checked out successfully
- Node.js environment was configured
- Dependencies installed without errors
- All tests passed

---

## Next Steps

1. **Experiment with your pipeline:**
   - Add more tests
   - Try different Node.js versions
   - Add code quality checks

2. **Learn about:**
   - Branch protection rules
   - Status checks
   - GitHub environments and secrets

3. **Explore GitHub Marketplace:**
   - Find pre-built actions for common tasks
   - Deploy to various cloud platforms
   - Integrate with external services

4. **Practice workflow:**
   - Create feature branches
   - Make pull requests
   - See how CI runs on PRs before merging

---

## Summary

You've learned:
- ✅ Git basics and configuration
- ✅ Working with branches and remotes
- ✅ Essential Git commands
- ✅ CI/CD concepts
- ✅ Creating GitHub Actions workflows
- ✅ Understanding the YAML structure
- ✅ Navigating the GitHub Actions interface

Keep practicing and building more complex workflows as you progress in your DevOps journey!