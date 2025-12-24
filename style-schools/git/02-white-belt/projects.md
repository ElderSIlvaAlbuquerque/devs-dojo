# White Belt - Capstone Projects

Pick **ONE** project to complete before promotion to Yellow Belt.

---

## Project 1: Personal Portfolio with Git History

**Time**: 1-2 weeks  
**Difficulty**: ⭐ Beginner  
**Focus**: Clean commit history and branching

### Description

Build a personal portfolio website (or any project in your language of choice) with **perfect Git hygiene**. The goal is not the project complexity, but demonstrating proper Git workflow.

### Requirements

**Code**:

- [ ] Minimum 20 meaningful commits
- [ ] At least 3 feature branches created and merged
- [ ] README with project description and setup instructions
- [ ] `.gitignore` file (ignore dependencies, build artifacts)

**Git Skills**:

- [ ] Every commit has a descriptive message following conventional commits
- [ ] Commits are atomic (one logical change each)
- [ ] Clean history viewable with `git log --graph --oneline --all`
- [ ] No "WIP", "fix", or meaningless commit messages
- [ ] All features developed in branches, not directly on `main`

**Deliverables**:

- [ ] GitHub repository with clean history
- [ ] README documenting your Git workflow
- [ ] Screenshot of `git log --graph --oneline --all`

### Example Workflow

```bash
# Initial setup
git init
git commit -m "docs: Initial commit with README"

# Feature 1
git checkout -b feature/header
# ... work ...
git commit -m "feat: Add header component"
git checkout main
git merge feature/header

# Feature 2
git checkout -b feature/about-section
# ... work ...
git commit -m "feat: Add about section"
git commit -m "style: Improve about section layout"
git checkout main
git merge feature/about-section

# Continue for 3+ features...
```

### Evaluation Criteria

- **Commit Quality (40%)**: Every commit is meaningful, descriptive, atomic
- **Branching (30%)**: Proper use of feature branches
- **History (20%)**: Clean, linear history (no merge chaos)
- **Documentation (10%)**: README explains Git workflow used

---

## Project 2: Open Source Contribution Preparation

**Time**: 1-2 weeks  
**Difficulty**: ⭐⭐ Beginner-Intermediate  
**Focus**: Fork, branch, and PR workflow

### Description

Prepare to contribute to open source by practicing the full contribution workflow on your own repository, then make 1 real contribution.

### Requirements

**Setup**:

- [ ] Find an open source project you want to contribute to
- [ ] Create a practice repository that simulates the project structure
- [ ] Fork and clone your own practice repo
- [ ] Configure upstream remote

**Practice Workflow**:

- [ ] Create 5 different "feature branches" simulating real contributions
- [ ] Make commits following the project's contribution guidelines
- [ ] Simulate pull request workflow (branch → commits → merge)
- [ ] Practice rebasing branches

**Real Contribution**:

- [ ] Make 1 real contribution to an open source project:
  - Documentation improvement (easiest)
  - Bug fix
  - Small feature
- [ ] Follow their Git workflow exactly
- [ ] Create a real pull request

**Deliverables**:

- [ ] Practice repository showing 5+ simulated contributions
- [ ] Link to 1 real open source pull request (even if not merged)
- [ ] Document what you learned about Git workflows

### Example Projects to Contribute To

- **Documentation**: Find typos in popular projects
- **Good First Issue**: Search GitHub for "good-first-issue" label
- **Small Projects**: Find projects with < 100 stars (more responsive maintainers)

### Evaluation Criteria

- **Practice Workflow (40%)**: Demonstrates fork/clone/branch/PR workflow
- **Commit Quality (30%)**: Follows target project's guidelines
- **Real Contribution (20%)**: Actually submitted a PR
- **Learning (10%)**: Documents workflow differences from personal projects

---

## Project 3: Bug Fix History Challenge

**Time**: 1-2 weeks  
**Difficulty**: ⭐⭐ Intermediate  
**Focus**: Git history as debugging tool

### Description

Create a project with intentional bugs, then use Git history to track down and fix them. Demonstrate how Git helps with debugging.

### Requirements

**Phase 1: Setup**:

- [ ] Create a working application (API, CLI tool, web app, etc.)
- [ ] Make 15+ commits with good history
- [ ] Intentionally introduce 3 bugs in different commits
- [ ] Don't document where the bugs are

**Phase 2: Bug Hunting**:

- [ ] Use `git log` to explore history
- [ ] Use `git diff` to see what changed
- [ ] Use `git show` to inspect suspicious commits
- [ ] Use `git blame` to find who introduced each bug (it's you!)
- [ ] Create fix branches for each bug

**Phase 3: Documentation**:

- [ ] Document how you found each bug using Git
- [ ] Show the exact Git commands used
- [ ] Explain how Git history made debugging easier

**Deliverables**:

- [ ] Repository with commit history showing bugs and fixes
- [ ] Markdown document: "How I Used Git to Find and Fix 3 Bugs"
- [ ] Each bug fix in its own branch, merged with descriptive commit
- [ ] Annotated `git log` showing bug introduction and fix

### Example Bug Hunt Process

```bash
# Bug reported: "Feature X stopped working"
# When did it break?

git log --oneline
# Look for commits that might have affected Feature X

git show abc123
# Inspect suspicious commit

git blame src/feature-x.js
# Find which commit introduced the problematic line

git diff good-commit bad-commit
# Compare before/after

# Fix in new branch
git checkout -b fix/feature-x-bug
# ... fix ...
git commit -m "fix: Resolve null pointer in Feature X"
```

### Evaluation Criteria

- **Git Usage (40%)**: Demonstrates effective use of history for debugging
- **Documentation (30%)**: Clearly explains bug-hunting process
- **Commit Quality (20%)**: Clean history showing bug introduction and fixes
- **Thoroughness (10%)**: Found all 3 bugs using Git tools

---

## Project 4: Git Workflow Documentation

**Time**: 1 week  
**Difficulty**: ⭐ Beginner  
**Focus**: Understanding and teaching Git concepts

### Description

Create comprehensive documentation teaching Git to a complete beginner. The best way to learn is to teach.

### Requirements

**Content**:

- [ ] "Git for Complete Beginners" guide (Markdown)
- [ ] Cover all White Belt concepts
- [ ] Include code examples for every command
- [ ] Create visual diagrams (optional: use Mermaid)
- [ ] Include common mistakes and how to fix them

**Practice Repository**:

- [ ] Create accompanying repository with examples
- [ ] Each concept has its own branch demonstrating it
- [ ] README links to the guide

**Demonstration**:

- [ ] Teach 1 person Git using your guide (friend, colleague, online)
- [ ] Document their questions and update guide
- [ ] Include feedback in final version

**Deliverables**:

- [ ] Complete Git guide (minimum 2000 words)
- [ ] Example repository with demonstrations
- [ ] Feedback from 1 person who used your guide

### Topics to Cover

- What is version control?
- Git vs GitHub
- Basic workflow (add, commit, push)
- Branching and merging
- Viewing history
- Undoing changes
- Best practices

### Evaluation Criteria

- **Clarity (40%)**: Can a beginner understand it?
- **Completeness (30%)**: Covers all White Belt concepts
- **Examples (20%)**: Code examples for every concept
- **Feedback (10%)**: Shows improvement based on teaching experience

---

## Submission Guidelines

For any project:

1. **Create GitHub repository**
2. **README must include**:
   - Project description
   - Git workflow used
   - How to clone and run
   - What you learned about Git
3. **Git history must show**:
   - Meaningful commits
   - Proper branching
   - Clean history
4. **Self-assessment**:
   - Complete [checklist.md](./checklist.md)
   - Note areas for improvement

---

## Promotion Criteria

To advance to Yellow Belt, your project must demonstrate:

- ✅ 20+ meaningful commits with conventional commit format
- ✅ 3+ feature branches properly merged
- ✅ Clean `git log` history (no "WIP" or "fix" messages)
- ✅ Proper use of `.gitignore`
- ✅ README documenting Git workflow
- ✅ Can explain every Git command used in project

---

**Next**: [Promotion Checklist](./checklist.md)
