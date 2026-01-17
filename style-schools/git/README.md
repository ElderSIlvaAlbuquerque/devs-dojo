# Git Style School

Mastering Version Control Throughout Your Career

---

## Overview

Git is the universal version control system that every developer must master. This style school teaches Git concepts progressively, from basic commands to advanced workflows and collaborative patterns used in professional teams.

Unlike language-specific schools, Git is **essential for all belts** and integrates with every project you build.

---

## Philosophy

```
Git mastery is NOT about memorizing commands.
It's about understanding:

✅ How version control enables collaboration
✅ When to commit and what makes a good commit
✅ How to handle conflicts and mistakes gracefully
✅ How teams coordinate using Git workflows
✅ How to maintain clean project history
```

---

## Belt Progression

### White Belt 🕊️

**Focus**: Basic Git operations and local workflow

**You'll Learn**:

- Initialize repositories
- Stage and commit changes
- View history and diffs
- Create and switch branches
- Basic merge operations

### Yellow Belt 💛

**Focus**: Collaboration and remote workflows

**You'll Learn**:

- Remote repositories (GitHub, GitLab)
- Push and pull operations
- Pull requests and code reviews
- Handling merge conflicts
- Branch protection rules

### Orange Belt 🧡

**Focus**: Team workflows and best practices

**You'll Learn**:

- Git Flow and trunk-based development
- Feature branch strategies
- Rebasing vs merging
- Interactive rebase for clean history
- Cherry-picking commits

### Green Belt 💚

**Focus**: Advanced Git operations

**You'll Learn**:

- Reflog and recovering lost work
- Bisect for debugging
- Submodules and subtrees
- Hooks for automation
- Advanced conflict resolution

### Blue Belt 💙

**Focus**: Repository architecture and scaling

**You'll Learn**:

- Monorepo strategies
- Git LFS for large files
- CI/CD integration patterns
- Branch strategies at scale
- Repository organization

### Brown Belt 🤎

**Focus**: Team leadership and Git practices

**You'll Learn**:

- Defining team Git standards
- Code review best practices
- Mentoring juniors on Git
- Troubleshooting team Git issues
- Git security and access control

### Black Belt ⚫

**Focus**: Organizational Git strategy

**You'll Learn**:

- Multi-repository architectures
- Migrating version control systems
- Git performance optimization
- Custom tooling and automation
- Git workflow RFC authoring

---

## Getting Started

1. **Install Git**: https://git-scm.com/downloads
2. **Configure Git**:
   ```bash
   git config --global user.name "Your Name"
   git config --global user.email "your@email.com"
   git config --global init.defaultBranch main
   ```
3. **Start with White Belt**: `02-white-belt/README.md`

---

## Quick Reference

### Essential Commands by Belt

**White Belt**:

```bash
git init
git add .
git commit -m "message"
git status
git log
git branch
git checkout
git merge
```

**Yellow Belt**:

```bash
git clone
git remote add
git push
git pull
git fetch
git pull --rebase
```

**Orange Belt**:

```bash
git rebase
git rebase -i
git cherry-pick
git stash
```

**Green Belt**:

```bash
git reflog
git bisect
git submodule
git blame
```

---

## Projects Integration

Every capstone project across all belts should demonstrate:

- ✅ Clean commit history
- ✅ Meaningful commit messages
- ✅ Proper branching strategy
- ✅ Code reviews via pull requests
- ✅ Version tags for releases

---

**Next**: Start with [White Belt Git Basics](02-white-belt/README.md)
