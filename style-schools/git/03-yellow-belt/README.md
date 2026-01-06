# Yellow Belt - Git Collaboration 💛

**Duration**: Week 3-4  
**Level**: Junior Developer  
**Prerequisites**: White Belt completed

---

## Learning Objectives

By the end of Yellow Belt, you will:

- ✅ Work with remote repositories (GitHub, GitLab)
- ✅ Push and pull code safely
- ✅ Create and review pull requests
- ✅ Resolve merge conflicts
- ✅ Understand branch protection rules
- ✅ Follow team collaboration workflows

---

## Core Concepts

### 1. Remote Repositories

A remote is a hosted version of your repository (GitHub, GitLab, Bitbucket). It enables:

- **Backup**: Code stored off your machine
- **Collaboration**: Multiple people working together
- **Deployment**: CI/CD systems deploy from remotes
- **Portfolio**: Public repos showcase your work

### 2. Fork vs Clone

```
Fork: Copy someone else's repo to your account (for contributing)
Clone: Download a repo to your local machine (for working)
```

### 3. Pull Request Workflow

```
1. Create feature branch
2. Make commits
3. Push to remote
4. Open pull request (PR)
5. Code review
6. Address feedback
7. Merge to main
```

---

## Key Commands

### Remote Operations

```bash
git remote add origin <url>     # Add remote repository
git remote -v                   # List remotes
git push -u origin main         # Push and set upstream
git push                        # Push to upstream branch
git pull                        # Fetch + merge from remote
git fetch                       # Download changes (no merge)
git pull --rebase               # Pull with rebase instead of merge
```

### Branch Management

```bash
git push origin <branch>        # Push branch to remote
git push -d origin <branch>     # Delete remote branch
git branch -r                   # List remote branches
git branch -a                   # List all branches (local + remote)
```

### Collaboration

```bash
git clone <url>                 # Clone repository
git fork                        # Fork via GitHub CLI
gh pr create                    # Create PR (GitHub CLI)
gh pr list                      # List PRs
gh pr checkout <number>         # Checkout PR locally
```

---

## Lessons

### Lesson 1: Working with Remotes

**What You'll Learn**:

- [ ] How to connect local repo to GitHub
- [ ] Push and pull operations
- [ ] Understanding origin and upstream

**Core Ideas**:

#### 1. Adding a Remote

```bash
# Create repo on GitHub first, then:
git remote add origin https://github.com/username/repo.git

# Verify
git remote -v
# Shows:
# origin  https://github.com/username/repo.git (fetch)
# origin  https://github.com/username/repo.git (push)
```

#### 2. First Push

```bash
git push -u origin main
# -u sets upstream tracking
# Now 'git push' will push to origin/main automatically
```

#### 3. Pulling Changes

```bash
git pull origin main
# Downloads changes and merges them

# Or separately:
git fetch origin        # Download
git merge origin/main   # Merge
```

**Why This Matters**:
Every professional team uses remote repositories. Understanding push/pull is fundamental to collaboration.

**Common Mistakes**:

- Forgetting to pull before starting work (causes conflicts)
- Pushing directly to main (should use branches)
- Not setting upstream with `-u` (have to type origin/branch every time)

---

### Lesson 2: Pull Requests

**What You'll Learn**:

- [ ] How to create a pull request
- [ ] PR description best practices
- [ ] Code review process
- [ ] Addressing review feedback

**Core Ideas**:

#### 1. Creating a PR

```bash
# 1. Create feature branch
git checkout -b feature/user-auth

# 2. Make commits
git commit -m "feat: Add user registration"
git commit -m "test: Add auth tests"

# 3. Push to remote
git push -u origin feature/user-auth

# 4. Open PR on GitHub
# Go to GitHub → "Compare & pull request"
```

#### 2. Good PR Description Template

```markdown
## What

Brief description of changes

## Why

Explain the problem being solved

## How

Explain your approach

## Testing

How to test these changes

## Screenshots (if applicable)

## Checklist

- [ ] Tests added/updated
- [ ] Documentation updated
- [ ] No breaking changes
```

#### 3. Code Review Process

```
1. Reviewer examines code
2. Leaves comments/suggestions
3. Author addresses feedback
4. Author pushes new commits
5. Reviewer approves
6. PR merged to main
```

**Why This Matters**:
PRs are how professional teams review and improve code quality before it reaches production.

**Common Mistakes**:

- PRs too large (aim for < 400 lines changed)
- Vague descriptions ("updates stuff")
- Taking review feedback personally (it's about the code, not you)
- Not testing before opening PR

---

### Lesson 3: Merge Conflicts

**What You'll Learn**:

- [ ] What causes merge conflicts
- [ ] How to resolve conflicts
- [ ] How to prevent conflicts
- [ ] Using merge tools

**Core Ideas**:

#### 1. What Causes Conflicts

```
Alice and Bob both edit line 5 of server.js
Alice: const port = 3000
Bob:   const port = 8080

When Bob tries to merge Alice's changes → CONFLICT!
```

#### 2. Resolving Conflicts

```bash
# After merge conflict:
git status
# Shows conflicted files

# Open file, you'll see:
<<<<<<< HEAD (your changes)
const port = 3000
=======
const port = 8080
>>>>>>> feature/new-port (their changes)

# Edit to resolve:
const port = 3000  # Choose one or combine

# Stage resolved file
git add server.js

# Complete merge
git commit
```

#### 3. Using Merge Tools

```bash
# Configure merge tool
git config --global merge.tool vscode
git config --global mergetool.vscode.cmd 'code --wait --merge $REMOTE $LOCAL $BASE $MERGED'

# Use it
git mergetool
```

**Why This Matters**:
Conflicts are inevitable when multiple people work on the same codebase. Knowing how to resolve them confidently is essential.

**Prevention Tips**:

- Pull frequently (before starting work)
- Keep PRs small and focused
- Communicate with team about what you're working on
- Use feature branches

---

### Lesson 4: Branch Protection Rules

**What You'll Learn**:

- [ ] Why protect main branch
- [ ] How to configure branch protection
- [ ] Requiring reviews before merge
- [ ] Status checks and CI/CD

**Core Ideas**:

#### 1. Why Protect Main?

Protecting main prevents:

- Accidental direct commits
- Merging without review
- Deploying untested code
- Overwriting others' work

#### 2. Common Protection Rules

```
✅ Require pull request before merging
✅ Require 1+ approving reviews
✅ Require status checks to pass (CI/CD)
✅ Require branches to be up to date
✅ Block force pushes
✅ Block deletions
```

#### 3. Setting Up Protection (GitHub)

```
1. Repo Settings → Branches
2. Add rule for 'main'
3. Enable:
   - Require pull request reviews (1 approval)
   - Require status checks (CI tests)
   - Require conversation resolution
   - Block force pushes
4. Save changes
```

#### 4. Working with Protected Branches

```bash
# ❌ This will fail on protected main:
git checkout main
git commit -m "hotfix"
git push
# Error: Protected branch

# ✅ Correct workflow:
git checkout -b hotfix/critical-bug
git commit -m "fix: Critical bug"
git push -u origin hotfix/critical-bug
# Open PR → Get review → Merge
```

**Why This Matters**:
Professional teams use branch protection to maintain code quality and prevent production incidents.

**Real-World Example**:

```
Without protection:
- Junior dev pushes directly to main
- Breaks production
- Customers affected
- 2-hour incident

With protection:
- Junior dev opens PR
- Senior reviews, finds bug
- Bug fixed before merge
- Production stays stable
```

---

### Lesson 5: Code Review Best Practices

**What You'll Learn**:

- [ ] How to review code effectively
- [ ] Giving constructive feedback
- [ ] Receiving feedback gracefully
- [ ] Review checklist

**Core Ideas**:

#### 1. What to Look For

```
✅ Correctness: Does it work?
✅ Tests: Are edge cases covered?
✅ Readability: Can others understand it?
✅ Performance: Any obvious bottlenecks?
✅ Security: Any vulnerabilities?
✅ Style: Follows team conventions?
```

#### 2. Giving Feedback

```markdown
❌ Bad: "This is wrong"
✅ Good: "Consider using a map here for O(1) lookup instead of O(n)"

❌ Bad: "Why did you do it this way?"
✅ Good: "I'm curious about this approach. What were the trade-offs?"

❌ Bad: "You need to fix this"
✅ Good: "Suggestion: Extract this into a helper function for reusability"
```

#### 3. Prefixes for Comments

```
[nit]: Minor style suggestion (not blocking)
[question]: Seeking clarification
[suggestion]: Alternative approach
[blocking]: Must be addressed before merge
```

#### 4. Review Checklist

```markdown
- [ ] Code builds successfully
- [ ] Tests pass
- [ ] New code has tests
- [ ] No obvious bugs
- [ ] Follows team style guide
- [ ] Documentation updated
- [ ] No sensitive data (passwords, keys)
- [ ] No commented-out code
- [ ] Commit messages are clear
```

**Why This Matters**:
Code review is how teams share knowledge, maintain quality, and catch bugs before production.

**Common Mistakes**:

- Only looking for bugs (miss learning opportunities)
- Being too harsh (demotivating)
- Approving without really reading (defeats the purpose)
- Nitpicking style when there's a formatter

---

### Lesson 6: Collaborative Workflows

**What You'll Learn**:

- [ ] GitHub Flow
- [ ] GitFlow
- [ ] Trunk-based development
- [ ] When to use each

**Core Ideas**:

#### 1. GitHub Flow (Simple)

```
main (always deployable)
  ├── feature/user-auth
  ├── feature/payment
  └── hotfix/critical-bug

Workflow:
1. Branch from main
2. Work + commit
3. Open PR
4. Review + merge
5. Deploy main
```

**Best for**: Small teams, continuous deployment

#### 2. GitFlow (Structured)

```
main (production)
  ├── develop (staging)
  │     ├── feature/x
  │     └── feature/y
  └── hotfix/critical
      └── release/v1.2

Workflow:
1. Features branch from develop
2. Merge features to develop
3. Create release branch
4. Test release
5. Merge to main + tag
6. Hotfixes branch from main
```

**Best for**: Scheduled releases, large teams

#### 3. Trunk-Based Development

```
main (trunk)
  ├── short-lived feature branches (< 2 days)

Workflow:
1. Small branches from main
2. Merge quickly (same day)
3. Feature flags for incomplete work
4. Deploy main frequently
```

**Best for**: High-frequency deployment, experienced teams

**Why This Matters**:
Different teams use different workflows. Understanding the options helps you adapt to any team.

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

- [GitHub Flow Guide](https://guides.github.com/introduction/flow/)
- [Atlassian Git Tutorials](https://www.atlassian.com/git/tutorials)
- [How to Write a Good Pull Request](https://github.blog/2015-01-21-how-to-write-the-perfect-pull-request/)
- [Code Review Best Practices](https://google.github.io/eng-practices/review/)

---

**Next**: [Daily Exercises](./daily-exercises.md)
