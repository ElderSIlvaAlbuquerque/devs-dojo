# Orange Belt - Daily Exercises

**Duration**: 20-30 minutes per exercise  
**Goal**: Master advanced Git techniques and repository management

---

## Week 1: Git Internals & Objects

### Monday

**Focus**: Understanding Git objects

- [ ] **Exercise 1** (15 min): Explore Git objects

  ```bash
  # Create a new repo
  mkdir git-internals
  cd git-internals
  git init

  # Create and commit a file
  echo "Hello Git" > file.txt
  git add file.txt
  git commit -m "Initial commit"

  # Explore the .git directory
  find .git/objects -type f

  # Get commit hash and examine it
  git log --oneline
  git cat-file -t HEAD      # type
  git cat-file -p HEAD      # content

  # Examine tree and blob
  git cat-file -p HEAD^{tree}
  ```

- [ ] **Exercise 2** (15 min): Create objects manually
  - Create a blob with `git hash-object`
  - Create a tree with `git mktree`
  - Create a commit with `git commit-tree`

### Tuesday

**Focus**: Git hooks

- [ ] **Exercise** (30 min): Create useful hooks

  ```bash
  # Pre-commit hook: Check for debugging statements
  cat > .git/hooks/pre-commit << 'EOF'
  #!/bin/bash
  if git diff --cached | grep -E "console.log|debugger|binding.pry"; then
      echo "Error: Remove debugging statements before committing"
      exit 1
  fi
  EOF
  chmod +x .git/hooks/pre-commit

  # Test it
  echo "console.log('test')" > test.js
  git add test.js
  git commit -m "Test"  # Should fail

  # Create commit-msg hook: Enforce format
  cat > .git/hooks/commit-msg << 'EOF'
  #!/bin/bash
  if ! head -1 "$1" | grep -qE "^(feat|fix|docs|style|refactor|test|chore):"; then
      echo "Error: Commit message must start with type (feat|fix|docs|etc)"
      exit 1
  fi
  EOF
  chmod +x .git/hooks/commit-msg
  ```

### Wednesday

**Focus**: Git bisect for bug hunting

- [ ] **Exercise** (30 min): Find bug with bisect

  ```bash
  # Create repo with a bug introduced somewhere
  mkdir bisect-practice
  cd bisect-practice
  git init

  # Create 20 commits, introduce bug at commit 10
  for i in {1..20}; do
    echo "function test() { return $i; }" > code.js
    if [ $i -eq 10 ]; then
      echo "function test() { return null; }" > code.js  # Bug!
    fi
    git add code.js
    git commit -m "Commit $i"
  done

  # Use bisect to find the bug
  git bisect start
  git bisect bad HEAD
  git bisect good HEAD~19

  # At each step, test
  # git bisect good/bad
  # Continue until you find commit 10
  ```

### Thursday

**Focus**: Git worktrees

- [ ] **Exercise** (25 min): Work on multiple branches simultaneously

  ```bash
  # Create main project
  mkdir main-project
  cd main-project
  git init
  echo "main" > main.txt
  git add main.txt
  git commit -m "Initial"

  # Create feature branch
  git checkout -b feature/new-feature
  echo "feature" > feature.txt
  git add feature.txt
  git commit -m "Add feature"
  git checkout main

  # Create worktree for feature branch
  git worktree add ../feature-worktree feature/new-feature

  # Now you can work in both directories simultaneously
  cd ../feature-worktree
  # Make changes here

  cd ../main-project
  # Make changes here

  # List worktrees
  git worktree list

  # Remove worktree when done
  git worktree remove ../feature-worktree
  ```

### Friday

**Focus**: Git reflog recovery

- [ ] **Exercise** (20 min): Recover "lost" commits

  ```bash
  # Create commits
  echo "v1" > file.txt
  git add file.txt
  git commit -m "Version 1"

  echo "v2" > file.txt
  git commit -am "Version 2"

  echo "v3" > file.txt
  git commit -am "Version 3"

  # "Lose" commits with reset
  git reset --hard HEAD~2

  # Recover using reflog
  git reflog
  # Find the hash of "Version 3"
  git checkout -b recovered <hash>

  # Or cherry-pick
  git checkout main
  git cherry-pick <hash>
  ```

---

## Week 2: Repository Management & Optimization

### Monday

**Focus**: Git filter-repo for history rewriting

- [ ] **Exercise** (30 min): Remove sensitive data

  ```bash
  # Install git-filter-repo
  pip install git-filter-repo

  # Create repo with sensitive data
  mkdir filter-practice
  cd filter-practice
  git init

  echo "API_KEY=secret123" > .env
  git add .env
  git commit -m "Add config"

  # More commits
  echo "code" > app.js
  git add app.js
  git commit -m "Add app"

  # Remove .env from history
  git filter-repo --path .env --invert-paths

  # Verify it's gone
  git log --all --full-history -- .env
  ```

### Tuesday

**Focus**: Submodules

- [ ] **Exercise** (30 min): Add and manage submodule

  ```bash
  # Create main repo
  mkdir main-repo
  cd main-repo
  git init

  # Create submodule repo separately
  cd ..
  mkdir sub-repo
  cd sub-repo
  git init
  echo "submodule content" > README.md
  git add README.md
  git commit -m "Initial"

  # Add as submodule
  cd ../main-repo
  git submodule add ../sub-repo libs/sub-repo
  git commit -m "Add submodule"

  # Clone repo with submodules
  cd ..
  git clone main-repo main-repo-clone
  cd main-repo-clone
  git submodule init
  git submodule update
  ```

### Wednesday

**Focus**: GPG commit signing

- [ ] **Exercise** (25 min): Sign commits

  ```bash
  # Generate GPG key (if you don't have one)
  gpg --full-generate-key

  # List keys
  gpg --list-secret-keys --keyid-format LONG

  # Configure Git to use GPG
  git config --global user.signingkey <KEY_ID>
  git config --global commit.gpgsign true

  # Make signed commit
  echo "content" > file.txt
  git add file.txt
  git commit -m "Signed commit"

  # Verify signature
  git log --show-signature
  ```

### Thursday

**Focus**: Advanced rebase

- [ ] **Exercise** (30 min): Interactive rebase mastery

  ```bash
  # Create commits with various issues
  for i in {1..5}; do
    echo "content $i" > file$i.txt
    git add file$i.txt
    git commit -m "WIP $i"
  done

  # Interactive rebase to clean up
  git rebase -i HEAD~5

  # In editor:
  # - squash related commits
  # - reword commit messages
  # - reorder commits
  # - drop unnecessary commits
  # - fixup commits

  # Practice with --autosquash
  echo "fix" > file1.txt
  git commit -am "fixup! WIP 1"
  git rebase -i --autosquash HEAD~6
  ```

### Friday

**Focus**: Git performance optimization

- [ ] **Exercise** (25 min): Optimize repository

  ```bash
  # Check repo size
  git count-objects -vH

  # Garbage collection
  git gc --aggressive --prune=now

  # Remove unreachable objects
  git prune

  # Check if large files exist
  git rev-list --objects --all \
    | git cat-file --batch-check='%(objecttype) %(objectname) %(objectsize) %(rest)' \
    | sed -n 's/^blob //p' \
    | sort --numeric-sort --key=2 \
    | tail -n 10

  # Set up git-lfs for large files
  git lfs install
  git lfs track "*.png"
  git lfs track "*.zip"
  git add .gitattributes
  git commit -m "Track large files with LFS"
  ```

---

## Week 3: Advanced Workflows

### Monday-Friday

**Focus**: Build custom Git tools

Create scripts to automate common workflows:

- [ ] **Auto-cleanup script**: Delete merged branches
- [ ] **PR template generator**: Create consistent PRs
- [ ] **Commit analyzer**: Check commit quality
- [ ] **Branch naming enforcer**: Validate branch names
- [ ] **Release automation**: Tag and generate changelogs

---

Remember: These exercises build muscle memory for advanced Git operations you'll use in professional settings.
