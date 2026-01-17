# Orange Belt - Git Rebase & Advanced Workflows 🧡

**Duration**: Week 5-7  
**Level**: Junior → Mid-level Developer  
**Prerequisites**: Yellow Belt completed

---

## Learning Objectives

By the end of Orange Belt, you will:

- ✅ Master git rebase for clean history
- ✅ Use interactive rebase to rewrite history
- ✅ Understand when to rebase vs merge
- ✅ Implement Git Flow workflow
- ✅ Use trunk-based development
- ✅ Cherry-pick commits strategically
- ✅ Work with git hooks for automation

---

## Core Concepts

### 1. Rebase vs Merge

**Merge** (what you know):

```
Feature branch merges INTO main
Creates merge commit
Preserves complete history
```

**Rebase** (new skill):

```
Feature branch REPLAYS ON TOP OF main
No merge commit
Linear history
Cleaner git log
```

### 2. When to Use Each

| Scenario             | Use Merge | Use Rebase      |
| -------------------- | --------- | --------------- |
| Public branch (main) | ✅        | ❌ Never        |
| Feature branch       | ❌        | ✅ Keep updated |
| Collaboration branch | ✅        | ⚠️ Careful      |
| Local only branch    | Either    | ✅ Preferred    |

### 3. Interactive Rebase

Rewrite history to:

- Combine commits (squash)
- Edit commit messages
- Reorder commits
- Remove commits
- Edit past commits

---

## Key Commands

### Rebase Basics

```bash
git rebase main                 # Replay current branch on main
git rebase --continue           # Continue after resolving conflict
git rebase --abort              # Cancel rebase
git rebase --skip               # Skip problematic commit
```

### Interactive Rebase

```bash
git rebase -i HEAD~3            # Interactively rebase last 3 commits
git rebase -i main              # Interactively rebase onto main
```

### Cherry-pick

```bash
git cherry-pick <commit-hash>   # Apply specific commit
git cherry-pick <hash1> <hash2> # Apply multiple commits
git cherry-pick --continue      # Continue after conflict
git cherry-pick --abort         # Cancel cherry-pick
```

### Advanced Operations

```bash
git reflog                      # View history of HEAD movements
git reset --hard <commit>       # Reset to specific commit (dangerous!)
git revert <commit>             # Create commit that undoes another
git stash                       # Temporarily save changes
git stash pop                   # Restore stashed changes
```

---

## Lessons

### Lesson 1: Understanding Rebase

**What You'll Learn**:

- [ ] What rebase does under the hood
- [ ] When to use rebase vs merge
- [ ] How to rebase safely

**Core Ideas**:

#### 1. What Happens During Rebase

```bash
Before rebase:
      C---D  feature
     /
A---B---E---F  main

After git rebase main:
              C'--D'  feature
             /
A---B---E---F  main

# C and D are replayed as C' and D' on top of F
# Original C and D still exist (temporarily) in reflog
```

#### 2. Basic Rebase Workflow

```bash
# Update your feature branch with latest main

# 1. Fetch latest
git fetch origin

# 2. Checkout feature branch
git checkout feature/my-feature

# 3. Rebase onto main
git rebase origin/main

# 4. If conflicts, resolve them
# ... edit files ...
git add .
git rebase --continue

# 5. Force push (history changed)
git push --force-with-lease
```

#### 3. Golden Rule of Rebase

```
❌ NEVER rebase commits that exist on public/shared branches
✅ ONLY rebase commits that exist only in your local branch

Why? Rebase rewrites history. If others have your commits,
rewriting causes divergence and confusion.
```

**Why This Matters**:
Rebase keeps project history clean and linear, making it easier to understand what happened and when.

**Common Mistakes**:

- Rebasing public branches (breaks others' work)
- Force pushing without `--force-with-lease` (loses work)
- Panicking during conflicts (just `--abort` and try again)

---

### Lesson 2: Interactive Rebase

**What You'll Learn**:

- [ ] How to squash commits
- [ ] How to edit commit messages
- [ ] How to reorder commits
- [ ] How to split commits

**Core Ideas**:

#### 1. Starting Interactive Rebase

```bash
# Rebase last 3 commits
git rebase -i HEAD~3

# Or rebase all commits since branching from main
git rebase -i main
```

#### 2. Interactive Rebase Commands

```
pick   = keep commit as-is
reword = keep commit but edit message
edit   = stop for amending
squash = combine with previous commit
fixup  = squash but discard commit message
drop   = remove commit
```

#### 3. Example: Cleaning Up History

```bash
# Your messy history:
abc123 feat: Add user model
def456 WIP
ghi789 fix typo
jkl012 Add validation

# Start interactive rebase
git rebase -i HEAD~4

# Editor shows:
pick abc123 feat: Add user model
pick def456 WIP
pick ghi789 fix typo
pick jkl012 Add validation

# Change to:
pick abc123 feat: Add user model
fixup def456 WIP
fixup ghi789 fix typo
squash jkl012 Add validation

# Result: 1 clean commit instead of 4 messy ones
```

#### 4. Practical Scenario: Squashing Before PR

```bash
# You have 10 commits in your feature branch
# Squash them into 3 logical commits before merging

git rebase -i main

# Organize commits into logical groups:
# - Setup/infrastructure changes
# - Core feature implementation
# - Tests and documentation
```

**Why This Matters**:
Clean commit history makes code review easier and helps future developers understand why changes were made.

---

### Lesson 3: Git Flow Workflow

**What You'll Learn**:

- [ ] Git Flow branch structure
- [ ] Release management
- [ ] Hotfix workflow
- [ ] When Git Flow makes sense

**Core Ideas**:

#### 1. Git Flow Branch Structure

```
main (production)
  |
  ├── develop (integration)
  │     |
  │     ├── feature/user-auth
  │     ├── feature/payment
  │     └── feature/dashboard
  │
  ├── release/v1.2.0 (staging)
  │
  └── hotfix/critical-bug (emergency)
```

#### 2. Feature Development Flow

```bash
# Start feature from develop
git checkout develop
git pull
git checkout -b feature/new-dashboard

# Work on feature
git commit -m "feat: Add dashboard layout"
git commit -m "feat: Add dashboard widgets"

# Merge back to develop
git checkout develop
git merge feature/new-dashboard
git push origin develop
```

#### 3. Release Flow

```bash
# Create release branch from develop
git checkout develop
git checkout -b release/v1.2.0

# Only bug fixes on release branch
git commit -m "fix: Resolve bug in dashboard"

# When ready for production
git checkout main
git merge release/v1.2.0
git tag v1.2.0
git push origin main --tags

# Merge back to develop
git checkout develop
git merge release/v1.2.0
git push origin develop

# Delete release branch
git branch -d release/v1.2.0
```

#### 4. Hotfix Flow

```bash
# Production is broken!

# Branch from main
git checkout main
git checkout -b hotfix/critical-payment-bug

# Fix bug
git commit -m "fix: Resolve payment processing error"

# Merge to main
git checkout main
git merge hotfix/critical-payment-bug
git tag v1.2.1
git push origin main --tags

# Merge to develop
git checkout develop
git merge hotfix/critical-payment-bug
git push origin develop

# Delete hotfix branch
git branch -d hotfix/critical-payment-bug
```

**When to Use Git Flow**:

- ✅ Scheduled releases (monthly, quarterly)
- ✅ Multiple versions in production
- ✅ Large teams with dedicated release manager
- ❌ Continuous deployment
- ❌ Small teams
- ❌ Fast iteration

---

### Lesson 4: Trunk-Based Development

**What You'll Learn**:

- [ ] Trunk-based development principles
- [ ] Feature flags
- [ ] Short-lived branches
- [ ] Continuous integration practices

**Core Ideas**:

#### 1. Trunk-Based Structure

```
main (trunk) - always deployable
  |
  ├── feature/quick-change-1 (< 1 day)
  ├── feature/quick-change-2 (< 1 day)
  └── feature/quick-change-3 (< 1 day)
```

#### 2. Core Principles

```
1. All developers commit to main (trunk) daily
2. Feature branches are short-lived (< 2 days)
3. Use feature flags for incomplete work
4. Maintain high test coverage
5. CI runs on every commit
6. Main is always deployable
```

#### 3. Feature Flags Pattern

```javascript
// Incomplete feature hidden behind flag
if (featureFlags.isEnabled("new-dashboard")) {
  return <NewDashboard />;
} else {
  return <OldDashboard />;
}

// Ship code to main, but not visible to users
// Toggle flag when ready
```

#### 4. Workflow

```bash
# Morning
git checkout main
git pull

# Create short-lived branch
git checkout -b feature/quick-fix

# Work for a few hours
git commit -m "feat: Add quick improvement"

# Merge same day
git checkout main
git pull
git merge feature/quick-fix
git push

# Or even better: use git rebase for linear history
git checkout feature/quick-fix
git rebase main
git checkout main
git merge feature/quick-fix --ff-only
git push
```

**Benefits**:

- Fast feedback (changes hit main quickly)
- Less merge conflict pain
- Encourages small, testable changes
- Easier to identify breaking changes

**Challenges**:

- Requires discipline
- Need good feature flags infrastructure
- High test coverage essential
- Not suitable for all team sizes

---

### Lesson 5: Cherry-Picking Commits

**What You'll Learn**:

- [ ] What cherry-pick does
- [ ] When to cherry-pick
- [ ] How to cherry-pick safely

**Core Ideas**:

#### 1. What is Cherry-Pick?

```
Apply a specific commit from one branch to another
WITHOUT merging the entire branch
```

#### 2. When to Cherry-Pick

```
✅ Apply hotfix to multiple branches
✅ Move commit to correct branch
✅ Backport feature to older version
❌ Regular feature development (use merge/rebase)
```

#### 3. Basic Cherry-Pick

```bash
# You made a commit on wrong branch
git checkout wrong-branch
git log --oneline
# abc123 fix: Important bugfix

# Apply to correct branch
git checkout correct-branch
git cherry-pick abc123

# Commit abc123 now exists on both branches
```

#### 4. Cherry-Pick Multiple Commits

```bash
# Apply commits def456, ghi789, jkl012
git cherry-pick def456 ghi789 jkl012

# Or apply range
git cherry-pick def456..jkl012
```

#### 5. Real-World Scenario: Hotfix to Multiple Versions

```bash
# Fixed bug in v2.0
git checkout release/v2.0
git commit -m "fix: Critical security issue"
# Commit: abc123

# Apply to v1.9 (still supported)
git checkout release/v1.9
git cherry-pick abc123

# Apply to main
git checkout main
git cherry-pick abc123

# Same fix now in 3 branches
```

**Common Issues**:

```bash
# Conflict during cherry-pick
git cherry-pick abc123
# CONFLICT

# Resolve conflict
# ... edit files ...
git add .
git cherry-pick --continue

# Or abort
git cherry-pick --abort
```

---

### Lesson 6: Git Hooks for Automation

**What You'll Learn**:

- [ ] What git hooks are
- [ ] Common hook use cases
- [ ] How to create hooks
- [ ] Team hooks with Husky

**Core Ideas**:

#### 1. What Are Git Hooks?

```
Scripts that run automatically at Git events:
- Before commit
- After commit
- Before push
- After merge
- etc.
```

#### 2. Common Hooks

```
pre-commit:  Run tests, lint code
commit-msg:  Validate commit message format
pre-push:    Run full test suite
post-merge:  Install dependencies
```

#### 3. Creating a Hook

```bash
# Navigate to hooks directory
cd .git/hooks

# Create pre-commit hook
cat > pre-commit << 'EOF'
#!/bin/sh

# Run tests before commit
npm test

# If tests fail, prevent commit
if [ $? -ne 0 ]; then
  echo "Tests failed. Commit aborted."
  exit 1
fi
EOF

# Make executable
chmod +x pre-commit
```

#### 4. Using Husky (Team Hooks)

```bash
# Install Husky
npm install --save-dev husky

# Initialize
npx husky install

# Add pre-commit hook
npx husky add .husky/pre-commit "npm test"

# Add commit-msg hook
npx husky add .husky/commit-msg 'npx --no -- commitlint --edit "$1"'

# Now all team members get same hooks
```

#### 5. Practical Examples

```bash
# Pre-commit: Check for console.log
cat > .git/hooks/pre-commit << 'EOF'
#!/bin/sh
if git diff --cached | grep -q "console.log"; then
  echo "Error: console.log found in commit"
  exit 1
fi
EOF

# Pre-commit: Run formatter
cat > .git/hooks/pre-commit << 'EOF'
#!/bin/sh
npm run format
git add -u
EOF

# Pre-push: Run full test suite
cat > .git/hooks/pre-push << 'EOF'
#!/bin/sh
npm run test:full
EOF
```

---

## Daily Exercises

See [daily-exercises.md](./daily-exercises.md)

---

## Projects

See [projects.md](./projects.md)

---

## Promotion Checklist

See [checklist.md](./checklist.md)

---

## Resources

- [Git Rebase Tutorial](https://www.atlassian.com/git/tutorials/rewriting-history/git-rebase)
- [Git Flow Cheatsheet](https://danielkummer.github.io/git-flow-cheatsheet/)
- [Trunk-Based Development](https://trunkbaseddevelopment.com/)
- [Git Hooks Documentation](https://git-scm.com/book/en/v2/Customizing-Git-Git-Hooks)
- [Husky](https://typicode.github.io/husky/)

---

**Next**: [Daily Exercises](./daily-exercises.md)
