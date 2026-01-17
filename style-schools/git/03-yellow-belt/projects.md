# Yellow Belt - Capstone Projects

Pick **ONE** project to complete before promotion to Orange Belt.

---

## Project 1: Open Source Contribution

**Time**: 2-3 weeks  
**Difficulty**: ⭐⭐ Intermediate  
**Focus**: Real-world collaboration workflow

### Description

Make meaningful contributions to open source projects, demonstrating mastery of Git collaboration workflows.

### Requirements

**Code**:

- [ ] Find 2-3 open source projects that accept contributions
- [ ] Read their CONTRIBUTING.md guidelines
- [ ] Complete at least 2 merged pull requests
- [ ] At least one PR should fix an issue or add a feature

**Git Skills**:

- [ ] Fork repositories correctly
- [ ] Keep fork synced with upstream
- [ ] Create feature branches following project conventions
- [ ] Write commits following project style guides
- [ ] Respond to code review feedback
- [ ] Rebase or squash commits as requested
- [ ] Handle merge conflicts if they arise

**Deliverables**:

- [ ] Links to merged PRs
- [ ] Documentation of your contribution process
- [ ] Screenshots of code review discussions
- [ ] Reflection on what you learned

### Example Workflow

```bash
# Fork on GitHub, then clone
git clone https://github.com/YOUR_USERNAME/project.git
cd project

# Add upstream remote
git remote add upstream https://github.com/ORIGINAL_OWNER/project.git

# Create feature branch
git checkout -b fix-typo-in-readme

# Make changes and commit
git add README.md
git commit -m "docs: Fix typo in installation section"

# Push and create PR
git push -u origin fix-typo-in-readme

# After review feedback, make changes
git add README.md
git commit -m "docs: Address review feedback"
git push

# Keep branch updated with upstream
git fetch upstream
git rebase upstream/main
git push --force-with-lease
```

### Evaluation Criteria

- **Contribution Quality (40%)**: Meaningful, useful contributions
- **Git Workflow (30%)**: Proper fork/branch/PR workflow
- **Collaboration (20%)**: Professional communication in PRs
- **Documentation (10%)**: Clear reflection on process

---

## Project 2: Team Collaboration Simulation

**Time**: 2-3 weeks  
**Difficulty**: ⭐⭐ Intermediate  
**Focus**: Team workflow and conflict resolution

### Description

Work with 2-3 peers on a shared project, practicing real team Git workflows including pull requests, code reviews, and conflict resolution.

### Requirements

**Setup**:

- [ ] Choose a project (web app, API, CLI tool, etc.)
- [ ] One person creates main repository
- [ ] All team members fork or are added as collaborators
- [ ] Establish branching strategy (feature branches, main protected)

**Collaboration**:

- [ ] Each person works on separate features
- [ ] Create at least 5 pull requests per person
- [ ] Review each other's PRs with constructive feedback
- [ ] Experience and resolve at least 3 merge conflicts
- [ ] Practice rebasing feature branches

**Process**:

- [ ] Use GitHub Issues to track work
- [ ] Link PRs to issues
- [ ] Use PR templates for consistency
- [ ] Require reviews before merging
- [ ] Keep main branch always deployable

**Deliverables**:

- [ ] Working project with clean Git history
- [ ] At least 15 total merged PRs
- [ ] Documentation of branching strategy
- [ ] Screenshots of conflict resolution
- [ ] Team retrospective document

### Example Team Workflow

```bash
# Team member 1 - Feature A
git checkout -b feature/user-authentication
# ... work ...
git push -u origin feature/user-authentication
# Open PR, request review

# Team member 2 - Feature B
git checkout -b feature/database-setup
# ... work ...
git push -u origin feature/database-setup
# Open PR, request review

# Reviewing
# - Check out PR branch locally
# - Test the feature
# - Leave comments on GitHub
# - Request changes or approve

# Handling conflicts
git fetch origin
git rebase origin/main
# Fix conflicts
git add .
git rebase --continue
git push --force-with-lease
```

### Evaluation Criteria

- **Collaboration (35%)**: Effective teamwork and communication
- **Git Workflow (35%)**: Proper branch/PR/review workflow
- **Conflict Resolution (20%)**: Successfully resolved conflicts
- **Documentation (10%)**: Clear process documentation

---

## Project 3: Repository Maintenance and Cleanup

**Time**: 1-2 weeks  
**Difficulty**: ⭐⭐ Intermediate  
**Focus**: Advanced Git operations and history management

### Description

Take an existing messy repository (or create one intentionally messy) and clean it up using advanced Git techniques.

### Requirements

**Initial Setup**:

- [ ] Start with a repository that has:
  - Messy commit history (WIP commits, unclear messages)
  - Large binary files committed by mistake
  - Sensitive data that needs removal
  - Divergent branches needing reconciliation
  - Old feature branches not cleaned up

**Cleanup Tasks**:

- [ ] Rebase and squash commits for cleaner history
- [ ] Remove large files from Git history
- [ ] Remove sensitive data (API keys, passwords)
- [ ] Merge or delete stale branches
- [ ] Write clear commit messages following conventions
- [ ] Set up .gitignore properly
- [ ] Create release tags

**Advanced Git**:

- [ ] Use `git filter-branch` or `git filter-repo`
- [ ] Interactive rebase with fixup/squash
- [ ] Cherry-pick useful commits
- [ ] Use `git reflog` to recover "lost" commits
- [ ] Clean up with `git gc` and `git prune`

**Deliverables**:

- [ ] Before/after repository comparison
- [ ] Documentation of all cleanup operations
- [ ] Script for automated cleanup tasks
- [ ] New CONTRIBUTING.md with Git guidelines
- [ ] Clean, linear history with clear releases

### Example Cleanup Operations

```bash
# Interactive rebase to squash commits
git rebase -i HEAD~10

# Remove large file from history
git filter-repo --path large-file.zip --invert-paths

# Remove sensitive data
git filter-repo --path config/secrets.yml --invert-paths

# Recover accidentally deleted branch
git reflog
git checkout -b recovered-branch abc1234

# Clean up local repository
git fetch --prune
git gc --aggressive
git prune

# Delete merged branches
git branch --merged | grep -v "main" | xargs git branch -d
```

### Evaluation Criteria

- **History Cleanup (40%)**: Successfully cleaned commit history
- **Advanced Git (30%)**: Proper use of advanced Git commands
- **Documentation (20%)**: Clear documentation of operations
- **Prevention (10%)**: Guidelines to prevent future mess

---

Choose one project, complete it thoroughly, and document your learning journey.
