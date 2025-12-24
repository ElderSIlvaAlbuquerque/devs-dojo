# White Belt - Git Basics 🕊️

**Duration**: Week 1-2  
**Level**: Beginner  
**Prerequisites**: None

---

## Learning Objectives

By the end of White Belt, you will:

- ✅ Understand what version control is and why it matters
- ✅ Create and manage local Git repositories
- ✅ Make meaningful commits with good messages
- ✅ Create and switch between branches
- ✅ Perform basic merges
- ✅ View project history and differences

---

## Core Concepts

### 1. What is Git?

Git is a distributed version control system that tracks changes to your code over time. It enables:

- **History**: See what changed, when, and why
- **Collaboration**: Work with others without conflicts
- **Safety**: Experiment without breaking working code
- **Accountability**: Know who made each change

### 2. The Three States

Files in Git exist in three states:

- **Working Directory**: Where you edit files
- **Staging Area (Index)**: Changes ready to commit
- **Repository (HEAD)**: Committed history

```
Working Directory → git add → Staging Area → git commit → Repository
```

### 3. Basic Workflow

```bash
# 1. Make changes to files
# 2. Stage changes
git add <file>

# 3. Commit with message
git commit -m "Descriptive message"

# 4. Repeat!
```

---

## Key Commands

### Initialize & Status

```bash
git init                    # Create new repository
git status                  # Check current state
git log                     # View commit history
git log --oneline           # Compact history view
```

### Staging & Committing

```bash
git add <file>              # Stage specific file
git add .                   # Stage all changes
git commit -m "message"     # Commit staged changes
git diff                    # View unstaged changes
git diff --staged           # View staged changes
```

### Branching

```bash
git branch                  # List branches
git branch <name>           # Create branch
git checkout <branch>       # Switch to branch
git checkout -b <branch>    # Create and switch
git merge <branch>          # Merge branch into current
```

### History & Information

```bash
git log                     # Full history
git log --graph --oneline   # Visual branch history
git show <commit>           # Show commit details
git blame <file>            # Who changed each line
```

---

## Good Commit Messages

### ❌ Bad Examples

```
git commit -m "fix"
git commit -m "updates"
git commit -m "asdf"
git commit -m "WIP"
```

### ✅ Good Examples

```
git commit -m "Add user authentication endpoint"
git commit -m "Fix null pointer error in payment service"
git commit -m "Update README with setup instructions"
git commit -m "Refactor database connection pooling"
```

### Format

```
<type>: <subject>

[optional body]

[optional footer]
```

**Types**: `feat`, `fix`, `docs`, `refactor`, `test`, `chore`

**Example**:

```
feat: Add user login endpoint

Implements POST /api/login with JWT authentication.
Includes input validation and rate limiting.

Closes #42
```

---

## Common Workflows

### Starting a New Project

```bash
mkdir my-project
cd my-project
git init
echo "# My Project" > README.md
git add README.md
git commit -m "Initial commit"
```

### Daily Development

```bash
# Check status
git status

# Make changes to files
# ...

# Stage changes
git add src/api.js

# Commit
git commit -m "Add error handling to API"

# View history
git log --oneline
```

### Creating a Feature Branch

```bash
# Create and switch to new branch
git checkout -b feature/user-auth

# Make changes and commit
git add .
git commit -m "Implement user authentication"

# Switch back to main
git checkout main

# Merge feature
git merge feature/user-auth
```

---

## Exercises

See [daily-exercises.md](./daily-exercises.md) for practice tasks.

---

## Projects

See [projects.md](./projects.md) for capstone project ideas.

---

## Promotion Requirements

See [checklist.md](./checklist.md) for what you need to demonstrate.

---

## Resources

- [Pro Git Book](https://git-scm.com/book/en/v2) - Free comprehensive guide
- [Git Cheat Sheet](https://education.github.com/git-cheat-sheet-education.pdf)
- [Learn Git Branching](https://learngitbranching.js.org/) - Interactive tutorial
- [Oh Shit, Git!?!](https://ohshitgit.com/) - Common mistakes and fixes

---

**Next**: [Daily Exercises](./daily-exercises.md)
