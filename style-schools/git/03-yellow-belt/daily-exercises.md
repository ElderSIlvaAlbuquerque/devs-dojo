# Yellow Belt - Daily Exercises

**Duration**: 15-25 minutes per exercise  
**Goal**: Master remote collaboration and pull request workflows

---

## Week 1: Remote Operations & Pull Requests

### Monday

**Focus**: Setting up remote repository

- [ ] **Exercise 1** (20 min): Create and push to GitHub

  ```bash
  # Create new local repo
  mkdir collab-practice
  cd collab-practice
  git init

  # Create files
  echo "# Collaboration Practice" > README.md
  git add README.md
  git commit -m "docs: Initial commit"

  # Create GitHub repo (via web or CLI)
  gh repo create collab-practice --public --source=. --remote=origin

  # Push
  git push -u origin main
  ```

- [ ] **Exercise 2** (10 min): Practice pull
  - Edit README on GitHub web interface
  - Pull changes locally with `git pull`
  - Verify changes appeared

### Tuesday

**Focus**: Feature branch + PR workflow

- [ ] **Exercise** (25 min): Complete PR workflow

  ```bash
  # Create feature branch
  git checkout -b feature/add-contributing

  # Add file
  echo "# Contributing Guide" > CONTRIBUTING.md
  git add CONTRIBUTING.md
  git commit -m "docs: Add contributing guidelines"

  # Push branch
  git push -u origin feature/add-contributing

  # Create PR on GitHub
  # Add description using template
  # Request review from yourself or friend
  ```

### Wednesday

**Focus**: Code review practice

- [ ] **Exercise 1** (15 min): Review someone's PR

  - Find an open source project
  - Look at open PRs
  - Practice leaving constructive comments (without submitting)
  - Focus on: correctness, tests, readability

- [ ] **Exercise 2** (10 min): Update your own PR
  - Make a change based on imagined feedback
  - Push additional commit to your PR branch
  - Observe how PR updates automatically

### Thursday

**Focus**: Merge conflicts

- [ ] **Exercise** (25 min): Create and resolve conflict

  ```bash
  # On main branch
  git checkout main
  echo "Version A" > conflict.txt
  git add conflict.txt
  git commit -m "Add conflict file - version A"
  git push

  # Create branch from BEFORE this commit
  git checkout HEAD~1
  git checkout -b feature/conflict-test
  echo "Version B" > conflict.txt
  git add conflict.txt
  git commit -m "Add conflict file - version B"
  git push -u origin feature/conflict-test

  # Try to merge main into your branch
  git merge main
  # Resolve conflict in conflict.txt
  # git add conflict.txt
  # git commit
  ```

### Friday

**Focus**: Branch protection setup

- [ ] **Exercise** (20 min): Configure branch protection
  ```
  1. Go to your repo Settings → Branches
  2. Add rule for 'main'
  3. Enable:
     - Require pull request before merging
     - Require approvals: 1
     - Require status checks (if you have CI)
     - Require conversation resolution
     - Block force pushes
  4. Test: Try to push directly to main (should fail)
  5. Verify: Must use PR workflow now
  ```

---

## Week 2: Advanced Collaboration

### Monday

**Focus**: Fork and contribute workflow

- [ ] **Exercise** (25 min): Practice fork workflow

  ```bash
  # Find a small open source repo or create practice repo
  # Fork it on GitHub

  # Clone YOUR fork
  git clone https://github.com/YOUR-USERNAME/repo-name
  cd repo-name

  # Add upstream remote
  git remote add upstream https://github.com/ORIGINAL-OWNER/repo-name

  # Create feature branch
  git checkout -b fix/typo-in-readme

  # Make change
  # ... edit README ...

  # Commit and push to YOUR fork
  git commit -m "docs: Fix typo in README"
  git push -u origin fix/typo-in-readme

  # Open PR from your fork to upstream
  ```

### Tuesday

**Focus**: Keeping fork in sync

- [ ] **Exercise** (15 min): Sync fork with upstream

  ```bash
  # Fetch upstream changes
  git fetch upstream

  # Checkout your main
  git checkout main

  # Merge upstream changes
  git merge upstream/main

  # Push to your fork
  git push origin main
  ```

### Wednesday

**Focus**: Multi-reviewer PR workflow

- [ ] **Exercise** (20 min): Simulate team review

  ```bash
  # Create PR that needs multiple reviews
  git checkout -b feature/important-change

  # Make substantial change
  echo "Major feature" > feature.txt
  git add feature.txt
  git commit -m "feat: Add major feature"
  git push -u origin feature/important-change

  # Open PR with detailed description:
  # - What: Feature description
  # - Why: Business justification
  # - How: Technical approach
  # - Testing: How to verify
  #
  # Request reviews from 2+ people
  # Practice addressing feedback
  ```

### Thursday

**Focus**: Handling stale branches

- [ ] **Exercise 1** (15 min): Update stale PR

  ```bash
  # Your feature branch is behind main
  git checkout feature/old-branch

  # Option 1: Merge main into feature
  git merge main
  # Resolve conflicts if any

  # Option 2: Rebase (cleaner history)
  git rebase main
  # Resolve conflicts if any
  git push --force-with-lease
  ```

- [ ] **Exercise 2** (10 min): Clean up merged branches

  ```bash
  # List all branches
  git branch -a

  # Delete local merged branches
  git branch -d feature/old-feature

  # Delete remote branch
  git push origin --delete feature/old-feature

  # Prune deleted remote branches
  git fetch --prune
  ```

### Friday

**Focus**: CI/CD integration

- [ ] **Exercise** (30 min): Add GitHub Actions

  ```yaml
  # Create .github/workflows/tests.yml
  name: Tests

  on:
    pull_request:
      branches: [main]
    push:
      branches: [main]

  jobs:
    test:
      runs-on: ubuntu-latest
      steps:
        - uses: actions/checkout@v3
        - name: Run tests
          run: |
            echo "Running tests..."
            # Add your test commands
  ```

  - Commit workflow file
  - Open PR
  - Watch status checks run
  - Observe how branch protection requires passing checks

---

## Week 3: Team Scenarios

### Scenario 1: Emergency Hotfix

```bash
# Production is broken, need quick fix

# 1. Branch from main
git checkout main
git pull
git checkout -b hotfix/critical-bug

# 2. Fix the bug
# ... make fix ...
git add .
git commit -m "fix: Resolve critical production bug"

# 3. Push and create PR
git push -u origin hotfix/critical-bug

# 4. Request urgent review
# 5. Merge immediately after approval
# 6. Verify fix in production
```

### Scenario 2: Large Feature with Multiple PRs

```bash
# Feature too large for one PR

# 1. Create parent branch
git checkout -b feature/user-management

# 2. Break into sub-features
git checkout -b feature/user-management-models
# ... implement models ...
git push -u origin feature/user-management-models
# Open PR to merge into feature/user-management (not main)

# 3. After models merged
git checkout feature/user-management
git checkout -b feature/user-management-api
# ... implement API ...
git push -u origin feature/user-management-api
# Open PR to merge into feature/user-management

# 4. After all sub-features merged
# Open PR to merge feature/user-management into main
```

### Scenario 3: Resolving Review Feedback

```bash
# Reviewer asked for changes

# Option 1: New commits (preserves history)
# ... make changes ...
git commit -m "refactor: Extract validation logic per review"
git push

# Option 2: Amend commit (cleaner)
# ... make changes ...
git commit --amend --no-edit
git push --force-with-lease

# Option 3: Fixup commits (cleanest)
# ... make changes ...
git commit --fixup <original-commit-hash>
git rebase -i --autosquash main
git push --force-with-lease
```

---

## Daily Habits for Collaboration

### Morning Routine

```bash
# Before starting work
git checkout main
git pull
git status
git branch -a  # See what branches exist
```

### Before Opening PR

```bash
# Checklist
git status              # Clean working directory?
git log --oneline       # Commit messages good?
git diff main           # Review all changes
# Run tests locally
# Update documentation if needed
```

### After PR Merged

```bash
# Clean up
git checkout main
git pull
git branch -d feature/merged-feature
git push origin --delete feature/merged-feature
```

---

## Quick Drills (5-10 minutes each)

### Drill 1: Speed PR

Time yourself completing full PR workflow:

1. Create branch
2. Make change
3. Commit
4. Push
5. Open PR on GitHub

Target: < 3 minutes

### Drill 2: Conflict Resolution

Create intentional conflict and resolve it:

1. Create two branches with conflicting changes
2. Merge and resolve
3. Time yourself
4. Try to beat your time

### Drill 3: Review Speed

Practice reviewing PRs quickly but thoroughly:

1. Find open source PRs
2. Review without submitting
3. Note: bugs, tests, style, suggestions
4. Time: 5 minutes per PR

---

## Self-Assessment

After 3-4 weeks, you should be able to:

- [ ] Push and pull without looking up commands
- [ ] Create PRs with good descriptions
- [ ] Resolve merge conflicts confidently
- [ ] Review code constructively
- [ ] Work with protected branches
- [ ] Keep branches in sync
- [ ] Use fork workflow for open source

---

**Next**: [Capstone Projects](./projects.md)
