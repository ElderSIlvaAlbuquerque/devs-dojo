# Orange Belt - Lessons

## Lesson 1: Git Internals - How Git Really Works

### What You'll Learn

- [ ] How Git stores data (objects, trees, blobs)
- [ ] The Git object model
- [ ] How commits are linked
- [ ] Understanding the .git directory

### Core Ideas

#### 1. Git Objects

Git stores everything as objects in `.git/objects/`:

```bash
# Four types of objects:
1. blob   - file content
2. tree   - directory structure
3. commit - snapshot with metadata
4. tag    - named reference to commit
```

#### 2. Content-Addressable Storage

```bash
# Git creates SHA-1 hash of content
echo "Hello World" | git hash-object --stdin
# => 557db03de997c86a4a028e1ebd3a1ceb225be238

# Content is stored at: .git/objects/55/7db03de997c86a4a028e1ebd3a1ceb225be238
```

#### 3. Commit Structure

```bash
$ git cat-file -p HEAD
tree 9c435a86e664be00db0d973e981425e4a3ef4657
parent 1a2b3c4d5e6f7g8h9i0j1k2l3m4n5o6p7q8r9s0t
author Name <email> 1234567890 -0400
committer Name <email> 1234567890 -0400

Commit message here
```

Each commit points to:
- A tree (directory snapshot)
- Parent commit(s)
- Metadata (author, timestamp)

#### 4. Trees and Blobs

```bash
$ git cat-file -p HEAD^{tree}
100644 blob 557db03    README.md
040000 tree 9c435a8    src/
100755 blob 1a2b3c4    script.sh
```

### Why This Matters

Understanding Git internals helps you:
- Debug complex issues
- Recover from disasters
- Use advanced features confidently
- Understand performance characteristics

### Common Mistakes

- Thinking Git stores diffs (it stores snapshots)
- Not understanding that branches are just pointers
- Fearing data loss (Git rarely loses data)

---

## Lesson 2: Git Hooks - Automating Workflows

### What You'll Learn

- [ ] Client-side vs server-side hooks
- [ ] Common hook use cases
- [ ] Writing effective hooks
- [ ] Sharing hooks with teams

### Core Ideas

#### 1. Client-Side Hooks

Located in `.git/hooks/`:

```bash
pre-commit       # Before commit is created
prepare-commit-msg # Before commit message editor
commit-msg       # Validate commit message
post-commit      # After commit is created
pre-push         # Before pushing
post-checkout    # After checkout
post-merge       # After merge
```

#### 2. Example: Enforce Commit Message Format

```bash
#!/bin/bash
# .git/hooks/commit-msg

commit_msg=$(cat "$1")

if ! echo "$commit_msg" | grep -qE "^(feat|fix|docs|style|refactor|test|chore): "; then
    echo "Error: Commit message must start with type: feat|fix|docs|style|refactor|test|chore"
    echo "Example: feat: Add user authentication"
    exit 1
fi

if [ ${#commit_msg} -lt 10 ]; then
    echo "Error: Commit message too short (minimum 10 characters)"
    exit 1
fi

exit 0
```

#### 3. Example: Pre-Commit Linting

```bash
#!/bin/bash
# .git/hooks/pre-commit

echo "Running pre-commit checks..."

# Run linter
npm run lint
if [ $? -ne 0 ]; then
    echo "Linting failed. Commit aborted."
    exit 1
fi

# Run tests
npm test
if [ $? -ne 0 ]; then
    echo "Tests failed. Commit aborted."
    exit 1
fi

echo "All checks passed!"
exit 0
```

#### 4. Sharing Hooks

Hooks in `.git/hooks/` aren't tracked by Git. Solutions:

```bash
# Store hooks in repo
mkdir .githooks
# Add hooks there
git config core.hooksPath .githooks

# Or use a hooks manager like Husky (Node.js)
npm install husky --save-dev
npx husky install
npx husky add .husky/pre-commit "npm test"
```

### Why This Matters

Hooks automate quality checks, preventing bad commits from entering the codebase.

---

## Lesson 3: Git Bisect - Binary Search for Bugs

### What You'll Learn

- [ ] How git bisect works
- [ ] Manual vs automated bisecting
- [ ] Writing bisect scripts
- [ ] Handling complex scenarios

### Core Ideas

#### 1. Binary Search for Bugs

When a bug exists but you don't know which commit introduced it:

```bash
# Start bisect
git bisect start

# Mark current as bad
git bisect bad HEAD

# Mark known good commit
git bisect good v1.0

# Git checks out middle commit
# Test it, then mark:
git bisect good   # or
git bisect bad

# Repeat until Git finds the culprit
```

#### 2. Automated Bisect

```bash
# Write a test script that exits 0 if good, 1 if bad
cat > test.sh << 'EOF'
#!/bin/bash
npm test
exit $?
EOF
chmod +x test.sh

# Run automated bisect
git bisect start HEAD v1.0
git bisect run ./test.sh

# Git will automatically find the bad commit
```

#### 3. Real Example

```bash
# Bug: Application crashes on startup
git bisect start
git bisect bad HEAD
git bisect good v2.1.0

# At each step:
npm start
# If it crashes: git bisect bad
# If it works: git bisect good

# Git output:
# abc1234 is the first bad commit
# commit abc1234
# Author: Dev Name
# Date:   Mon Jan 1 12:00:00 2024
#     refactor: Change initialization order
```

### Why This Matters

Bisect can find a bug-introducing commit in O(log n) time, even in repositories with thousands of commits.

---

## Lesson 4: Git Worktrees - Parallel Development

### What You'll Learn

- [ ] What worktrees are and when to use them
- [ ] Managing multiple worktrees
- [ ] Worktree best practices

### Core Ideas

#### 1. Problem: Switching Branches Interrupts Work

Traditional workflow:
```bash
# Working on feature
git checkout feature/new-ui
# Building, testing...

# Urgent hotfix needed!
git stash
git checkout main
git checkout -b hotfix/critical-bug
# Fix bug...
git checkout feature/new-ui
git stash pop
# Resume work
```

#### 2. Worktrees: Simultaneous Branch Access

```bash
# Create worktree
git worktree add ../hotfix hotfix/critical-bug

# Now you have two directories:
# ./project          (feature/new-ui branch)
# ../hotfix          (hotfix/critical-bug branch)

# Work in both simultaneously!
cd ../hotfix
# Fix bug, commit, push

cd -
# Continue feature work
```

#### 3. Worktree Management

```bash
# List worktrees
git worktree list

# Remove worktree
git worktree remove ../hotfix

# Prune deleted worktrees
git worktree prune

# Lock worktree (prevent pruning)
git worktree lock ../important-branch
```

#### 4. Use Cases

- **Urgent fixes**: Keep feature branch while fixing bugs
- **Testing**: Test different branches simultaneously
- **Build systems**: Build multiple branches in parallel
- **Code review**: Review PR without switching away from work

### Why This Matters

Worktrees eliminate the need for stashing or multiple clones, increasing productivity.

---

## Lesson 5: Git Reflog - The Safety Net

### What You'll Learn

- [ ] What reflog records
- [ ] Recovering lost commits
- [ ] Undoing dangerous operations
- [ ] Reflog expiration

### Core Ideas

#### 1. What Is Reflog?

Git records every update to HEAD:

```bash
$ git reflog
abc1234 HEAD@{0}: commit: Add feature
def5678 HEAD@{1}: checkout: moving from main to feature
9876543 HEAD@{2}: commit: Fix bug
```

#### 2. Recovering "Lost" Commits

```bash
# Accidentally reset
git reset --hard HEAD~5

# Oh no! Lost 5 commits!

# Find them in reflog
git reflog
# abc1234 HEAD@{1}: commit: Important work

# Recover
git cherry-pick abc1234
# Or create new branch
git checkout -b recovered abc1234
```

#### 3. Undoing Rebases

```bash
# Before rebase
git reflog
# note the commit hash

# Rebase went wrong
git rebase -i HEAD~10
# Messed up, aborted

# Find pre-rebase state
git reflog
# abc1234 HEAD@{5}: rebase (start)

# Reset to before rebase
git reset --hard HEAD@{5}
```

#### 4. Reflog Expiration

```bash
# Reflog entries expire after 90 days (default)
# Unreachable entries expire after 30 days

# See expiration settings
git config gc.reflogExpire        # 90 days
git config gc.reflogExpireUnreachable  # 30 days

# Keep reflog longer
git config gc.reflogExpire 180.days
```

### Why This Matters

Reflog is your safety net - Git rarely loses data permanently if you know about reflog.

---

## Lesson 6: Advanced Rebasing

### What You'll Learn

- [ ] Interactive rebase operations
- [ ] Rebase --onto
- [ ] Preserving merge commits
- [ ] Autosquash workflow

### Core Ideas

#### 1. Interactive Rebase Commands

```bash
git rebase -i HEAD~5

# In editor:
pick abc1234 Add feature
squash def5678 Fix typo in feature
reword 9876543 Update docs
edit fedcba9 Configure settings
drop 1234567 Remove debug code
```

Commands:
- `pick`: Keep commit as-is
- `reword`: Change commit message
- `edit`: Pause to amend commit
- `squash`: Combine with previous commit
- `fixup`: Like squash but discard message
- `drop`: Remove commit

#### 2. Rebase --onto

```bash
# Move commits from one base to another
git rebase --onto main feature-old feature-new

# Example: Extract commits
# Before: main--A--B--C--D--E (feature)
#                       ^F--G (hotfix)
# Extract F-G to be based on main:
git rebase --onto main feature hotfix
# Result: main--F--G (hotfix)
```

#### 3. Autosquash Workflow

```bash
# Make changes to previous commit
echo "fix" > file.txt
git add file.txt
git commit --fixup abc1234

# Later, rebase with autosquash
git rebase -i --autosquash main

# Git automatically marks fixup commits
# and reorders them appropriately
```

### Why This Matters

Advanced rebasing keeps history clean and makes it easier for teams to understand project evolution.

---

## Lesson 7: Submodules and Subtrees

### What You'll Learn

- [ ] Submodules vs subtrees
- [ ] When to use each
- [ ] Managing dependencies
- [ ] Common pitfalls

### Core Ideas

#### 1. Submodules

Track other repositories within your repository:

```bash
# Add submodule
git submodule add https://github.com/user/lib.git libs/lib

# Clone repo with submodules
git clone https://github.com/user/main.git
cd main
git submodule init
git submodule update

# Or in one command
git clone --recursive https://github.com/user/main.git

# Update submodule
cd libs/lib
git pull origin main
cd ../..
git add libs/lib
git commit -m "Update lib submodule"
```

Pros:
- Maintains separate history
- Easy to update to specific version

Cons:
- More complex to work with
- Easy to forget to update
- Cloning requires extra steps

#### 2. Subtrees

Merge another repository into a subdirectory:

```bash
# Add subtree
git subtree add --prefix=libs/lib https://github.com/user/lib.git main

# Update subtree
git subtree pull --prefix=libs/lib https://github.com/user/lib.git main

# Push changes back to lib
git subtree push --prefix=libs/lib https://github.com/user/lib.git main
```

Pros:
- Simpler for contributors (appears as regular code)
- No extra clone steps

Cons:
- History is merged
- More complex to extract changes

### When to Use Each

- **Submodules**: When you need precise version control of dependencies
- **Subtrees**: When you want simplicity for contributors

---

## Lesson 8: Monorepo Strategies

### What You'll Learn

- [ ] Monorepo vs polyrepo
- [ ] Performance optimization
- [ ] Sparse checkout
- [ ] Partial clones

### Core Ideas

#### 1. Sparse Checkout

Only checkout parts of repository:

```bash
# Enable sparse checkout
git clone --no-checkout https://github.com/user/monorepo.git
cd monorepo
git sparse-checkout init --cone

# Specify directories to include
git sparse-checkout set frontend/app1 shared/utils

# Checkout
git checkout main

# Only frontend/app1 and shared/utils are present
```

#### 2. Partial Clones

Clone without full history:

```bash
# Shallow clone (only latest commit)
git clone --depth 1 https://github.com/user/repo.git

# Partial clone (history but not all blobs)
git clone --filter=blob:none https://github.com/user/repo.git

# Fetch more history later
git fetch --deepen=100
```

#### 3. Performance Tips

```bash
# Enable multi-core operations
git config --global pack.threads 0

# Enable file system monitor
git config core.fsmonitor true

# Use commit-graph for faster operations
git config core.commitGraph true
git config gc.writeCommitGraph true
git commit-graph write --reachable

# Aggressive garbage collection
git gc --aggressive
```

### Why This Matters

Large repositories need optimization techniques to remain performant and practical.

---

Remember: These advanced techniques are powerful but complex. Always test in a safe environment before using in production repositories.
