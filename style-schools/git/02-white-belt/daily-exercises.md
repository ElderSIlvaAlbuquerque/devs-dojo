# White Belt - Daily Exercises

**Duration**: 15-25 minutes per exercise  
**Goal**: Build muscle memory for basic Git operations

---

## Week 1: Fundamentals

### Monday

**Focus**: Repository initialization and basic commits

- [ ] **Exercise 1** (15 min): Create a new repository

  ```bash
  mkdir git-practice-monday
  cd git-practice-monday
  git init
  echo "# Monday Practice" > README.md
  git add README.md
  git commit -m "Initial commit"
  ```

- [ ] **Exercise 2** (10 min): Make 5 commits
  - Create 5 different files
  - Commit each one separately with descriptive messages
  - View history with `git log --oneline`

### Tuesday

**Focus**: Staging and unstaging

- [ ] **Exercise 1** (15 min): Practice selective staging

  ```bash
  # Create multiple files
  touch file1.txt file2.txt file3.txt

  # Stage only file1
  git add file1.txt

  # Check status
  git status

  # Stage the rest
  git add .

  # Commit
  git commit -m "Add three files"
  ```

- [ ] **Exercise 2** (10 min): Practice unstaging
  - Make changes to 3 files
  - Stage all of them
  - Unstage one file
  - Commit only the staged files

### Wednesday

**Focus**: Viewing differences

- [ ] **Exercise 1** (20 min): Explore `git diff`

  ```bash
  # Make changes to a file
  echo "New line" >> README.md

  # View unstaged changes
  git diff

  # Stage it
  git add README.md

  # View staged changes
  git diff --staged

  # Commit
  git commit -m "Update README"
  ```

- [ ] **Exercise 2** (10 min): Compare commits
  - Make 3 commits
  - Use `git diff HEAD~2 HEAD` to compare

### Thursday

**Focus**: Branches basics

- [ ] **Exercise 1** (20 min): Create your first branch

  ```bash
  # Create and switch to new branch
  git checkout -b feature/hello

  # Make changes
  echo "Hello from feature branch" > hello.txt
  git add hello.txt
  git commit -m "Add hello file"

  # Switch back to main
  git checkout main

  # Notice hello.txt doesn't exist here
  ls

  # Switch back to feature
  git checkout feature/hello

  # Now it exists
  ls
  ```

- [ ] **Exercise 2** (5 min): List branches
  - Use `git branch` to see all branches
  - Notice the `*` indicates current branch

### Friday

**Focus**: Merging branches

- [ ] **Exercise 1** (25 min): Complete branch workflow

  ```bash
  # On main branch
  git checkout main

  # Create feature branch
  git checkout -b feature/calculator

  # Add code
  echo "def add(a, b): return a + b" > calculator.py
  git add calculator.py
  git commit -m "feat: Add calculator function"

  # Switch to main
  git checkout main

  # Merge feature
  git merge feature/calculator

  # View history
  git log --graph --oneline --all
  ```

---

## Week 2: Practice & Reinforcement

### Monday

**Focus**: Good commit messages

- [ ] **Exercise** (20 min): Practice conventional commits
  - Create a project with 10 commits
  - Use proper prefixes: `feat:`, `fix:`, `docs:`, `refactor:`
  - Example:
    ```bash
    git commit -m "feat: Add user registration"
    git commit -m "fix: Resolve null pointer error"
    git commit -m "docs: Update installation guide"
    git commit -m "refactor: Simplify validation logic"
    ```

### Tuesday

**Focus**: Git history exploration

- [ ] **Exercise 1** (15 min): Explore `git log` options

  ```bash
  git log --oneline
  git log --graph --oneline --all
  git log --author="YourName"
  git log --since="1 week ago"
  git log --grep="feat"
  ```

- [ ] **Exercise 2** (10 min): Use `git show`
  - Pick a commit from `git log`
  - View its details with `git show <commit-hash>`

### Wednesday

**Focus**: Undoing changes

- [ ] **Exercise 1** (15 min): Practice unstaging

  ```bash
  # Make changes to multiple files
  echo "Change 1" >> file1.txt
  echo "Change 2" >> file2.txt

  # Stage all
  git add .

  # Oops, don't want to commit file2 yet
  git restore --staged file2.txt

  # Commit only file1
  git commit -m "Update file1"
  ```

- [ ] **Exercise 2** (10 min): Discard changes

  ```bash
  # Make a change
  echo "Bad change" >> file1.txt

  # View diff
  git diff

  # Discard it
  git restore file1.txt

  # Verify it's gone
  git diff
  ```

### Thursday

**Focus**: Amending commits

- [ ] **Exercise** (20 min): Practice `--amend`

  ```bash
  # Make a commit with a typo
  git commit -m "feat: Add usre login"

  # Fix the message
  git commit --amend -m "feat: Add user login"

  # Or add forgotten changes
  echo "forgotten" > forgotten.txt
  git add forgotten.txt
  git commit --amend --no-edit
  ```

### Friday

**Focus**: Complete workflow simulation

- [ ] **Exercise** (30 min): Build a mini-project

  ```bash
  # Create new project
  mkdir todo-app
  cd todo-app
  git init

  # Main branch setup
  echo "# Todo App" > README.md
  git add README.md
  git commit -m "docs: Initial README"

  # Feature 1: Add todos
  git checkout -b feature/add-todo
  echo "Add todo functionality" > add_todo.py
  git add add_todo.py
  git commit -m "feat: Implement add todo"
  git checkout main
  git merge feature/add-todo

  # Feature 2: List todos
  git checkout -b feature/list-todos
  echo "List todos functionality" > list_todos.py
  git add list_todos.py
  git commit -m "feat: Implement list todos"
  git checkout main
  git merge feature/list-todos

  # View final history
  git log --graph --oneline --all
  ```

---

## Daily Habits

Build these habits every day:

1. **Before starting work**:

   ```bash
   git status    # Where am I?
   git branch    # Which branch?
   ```

2. **Before committing**:

   ```bash
   git status    # What's staged?
   git diff --staged  # What am I committing?
   ```

3. **After committing**:
   ```bash
   git log --oneline  # Did it work?
   ```

---

## Quick Drills (5 minutes each)

### Drill 1: Speed Commits

Time yourself making 5 commits with good messages. Try to beat your time.

### Drill 2: Branch Dance

```bash
git checkout -b test1
git checkout -b test2
git checkout -b test3
git checkout main
git branch -D test1 test2 test3
```

### Drill 3: Status Check

Run `git status` after every command. Build the habit of checking state frequently.

---

## Self-Assessment

After 2 weeks, you should be able to:

- [ ] Create a repository without looking up commands
- [ ] Make meaningful commits with good messages
- [ ] Create and merge branches confidently
- [ ] Use `git status` and `git diff` habitually
- [ ] Fix common mistakes (unstage, discard, amend)

---

**Next**: [Capstone Projects](./projects.md)
