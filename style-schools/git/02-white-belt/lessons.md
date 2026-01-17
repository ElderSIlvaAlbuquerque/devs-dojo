# White Belt - Lessons

## Lesson 1: Introduction to Version Control

### What You'll Learn

- [ ] What version control is and why it exists
- [ ] The difference between centralized and distributed VCS
- [ ] Why Git became the industry standard

### Core Ideas

#### 1. The Problem Version Control Solves

Without version control:

- "final_v2_ACTUAL_final.docx" naming chaos
- No way to see what changed between versions
- Hard to collaborate without overwriting each other's work
- No way to undo changes safely

#### 2. Centralized vs Distributed

- **Centralized** (SVN): One central server, everyone connects to it
- **Distributed** (Git): Everyone has full history locally

#### 3. Why Git Won

- Fast (most operations are local)
- Powerful branching and merging
- Distributed (work offline)
- Industry adoption (GitHub, GitLab, Bitbucket)

### Why This Matters

Every professional software team uses version control. Understanding Git is as fundamental as knowing how to code.

### Common Mistakes

- Thinking Git is the same as GitHub (Git = tool, GitHub = hosting service)
- Not committing frequently enough
- Treating Git like Dropbox (it's not automatic sync)

---

## Lesson 2: Git Basics - Your First Repository

### What You'll Learn

- [ ] How to initialize a repository
- [ ] The three states of Git (working, staging, committed)
- [ ] How to make your first commit

### Core Ideas

#### 1. Initializing a Repository

```bash
git init
# Creates .git/ directory that stores all version history
```

#### 2. The Three Trees

```
Working Directory (where you edit)
       ↓ git add
Staging Area (what will be committed)
       ↓ git commit
Repository (permanent history)
```

#### 3. Your First Commit

```bash
echo "# My Project" > README.md
git add README.md
git commit -m "Initial commit"
```

### Why This Matters

Understanding the three states prevents confusion about what Git is tracking vs what it's ignoring.

### Common Mistakes

- Committing too much at once (commit related changes together)
- Forgetting to `git add` before `git commit`
- Not checking `git status` before committing

### Practice

```bash
# Create a new project
mkdir git-practice
cd git-practice
git init

# Create some files
echo "Hello Git" > hello.txt
echo "# Practice Project" > README.md

# Check status
git status
# Should show "Untracked files"

# Stage files
git add hello.txt README.md

# Check status again
git status
# Should show "Changes to be committed"

# Commit
git commit -m "Add initial files"

# View history
git log
```

---

## Lesson 3: Commit Messages and History

### What You'll Learn

- [ ] How to write good commit messages
- [ ] Why commit messages matter
- [ ] How to view commit history

### Core Ideas

#### 1. Anatomy of a Good Commit Message

```
<type>: <short summary>

<optional detailed description>

<optional footer>
```

**Types**:

- `feat`: New feature
- `fix`: Bug fix
- `docs`: Documentation change
- `refactor`: Code restructuring (no behavior change)
- `test`: Adding or updating tests
- `chore`: Maintenance (dependencies, build, etc.)

#### 2. Why Messages Matter
When debugging, you'll use `git log` to find when a bug was introduced. Good messages help you understand **why** changes were made.

#### 3. Viewing History

```bash
git log                      # Full history
git log --oneline            # Compact view
git log --graph --oneline    # Visual branch structure
git log -n 5                 # Last 5 commits
git log --author="YourName"  # Your commits only
```

### Why This Matters

Six months from now, "fix bug" won't help you. "Fix null pointer in payment processing" will.

### Practice

```bash
# Make a change
echo "Git is awesome" >> hello.txt

# Stage and commit with good message
git add hello.txt
git commit -m "docs: Add enthusiasm to hello message"

# View history
git log --oneline
```

---

## Lesson 4: Branches - Parallel Development

### What You'll Learn

- [ ] What branches are and why they're powerful
- [ ] How to create and switch branches
- [ ] How to merge branches

### Core Ideas

#### 1. What is a Branch?

A branch is a pointer to a commit. It lets you:

- Work on features without affecting main code
- Experiment safely
- Collaborate without conflicts

#### 2. Creating and Switching

```bash
git branch feature/new-api    # Create branch
git checkout feature/new-api  # Switch to it

# Or in one command:
git checkout -b feature/new-api
```
#### 3. Merging

```bash
# Switch to branch you want to merge INTO
git checkout main

# Merge the feature branch
git merge feature/new-api
```

### Why This Matters

Professional teams use branches for:

- Feature development (feature branches)
- Bug fixes (hotfix branches)
- Releases (release branches)

### Common Mistakes

- Working directly on `main` branch
- Forgetting which branch you're on
- Not pulling latest changes before creating a branch

### Practice

```bash
# Check current branch
git branch

# Create feature branch
git checkout -b feature/add-goodbye

# Make changes
echo "Goodbye Git" > goodbye.txt
git add goodbye.txt
git commit -m "feat: Add goodbye message"

# Switch back to main
git checkout main

# Merge feature
git merge feature/add-goodbye

# View history with branches
git log --graph --oneline --all
```

---

## Lesson 5: Viewing Changes and Differences

### What You'll Learn

- [ ] How to see what changed
- [ ] How to compare commits
- [ ] How to see who changed what

### Core Ideas

#### 1. Viewing Unstaged Changes

```bash
git diff              # Changes not yet staged
git diff <file>       # Changes in specific file
```

#### 2. Viewing Staged Changes

```bash
git diff --staged     # Changes ready to commit
```

#### 3. Comparing Commits

```bash
git diff HEAD~1 HEAD           # Last commit vs current
git diff abc123 def456         # Between two commits
git diff main feature/new-api  # Between branches
```

#### 4. Who Changed What

```bash
git blame <file>      # Line-by-line authorship
git show <commit>     # Show specific commit
```

### Why This Matters

Before committing, always review what you're about to commit. `git diff` is your sanity check.

### Practice

```bash
# Make a change (don't commit yet)
echo "More content" >> README.md

# View the diff
git diff

# Stage it
git add README.md

# View staged diff
git diff --staged

# Commit
git commit -m "docs: Expand README"

# View the commit
git show HEAD
```

---

## Lesson 6: Undoing Changes

### What You'll Learn

- [ ] How to unstage files
- [ ] How to discard uncommitted changes
- [ ] How to amend the last commit

### Core Ideas

#### 1. Unstaging Files

```bash
git restore --staged <file>   # Unstage file (Git 2.23+)
git reset HEAD <file>          # Older Git versions
```

#### 2. Discarding Changes

```bash
git restore <file>             # Discard changes (Git 2.23+)
git checkout -- <file>         # Older Git versions
```

#### 3. Amending Last Commit

```bash
git commit --amend             # Edit last commit message
git commit --amend --no-edit   # Add changes to last commit
```

### Why This Matters

Mistakes happen. Knowing how to undo changes safely is essential.

### Common Mistakes

- Using `git reset --hard` without understanding it (you'll lose work!)
- Not checking `git status` before undoing
- Amending commits that were already pushed (causes problems for others)

### Practice

```bash
# Make a change
echo "Temporary" > temp.txt
git add temp.txt

# Oops, didn't mean to stage that
git restore --staged temp.txt

# Actually, don't want this file at all
rm temp.txt

# Make a commit with typo
git add README.md
git commit -m "feat: Add readm content"

# Fix the typo
git commit --amend -m "feat: Add readme content"
```

---

## Next Steps

Complete the [daily exercises](./daily-exercises.md) and pick a [capstone project](./projects.md).
