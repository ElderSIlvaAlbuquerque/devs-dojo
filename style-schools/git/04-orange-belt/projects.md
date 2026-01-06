# Orange Belt - Capstone Projects

Pick **ONE** project to complete before promotion to Brown Belt.

---

## Project 1: Git Automation Framework

**Time**: 3-4 weeks  
**Difficulty**: ⭐⭐⭐ Advanced  
**Focus**: Custom tooling and automation

### Description

Build a comprehensive Git automation framework with hooks, scripts, and tools that enforce best practices and automate common workflows.

### Requirements

**Git Hooks**:

- [ ] Pre-commit: Lint code, check for secrets, enforce file size limits
- [ ] Commit-msg: Validate commit message format, enforce conventional commits
- [ ] Pre-push: Run tests, check branch naming, prevent force push to main
- [ ] Post-commit: Auto-generate documentation, update changelog
- [ ] Post-merge: Clean up dependencies, update submodules

**Custom Scripts**:

- [ ] Branch management tool (list, clean, rename following conventions)
- [ ] Release automation (tag, changelog, version bump)
- [ ] PR template generator with automatic label suggestion
- [ ] Commit quality analyzer (check message quality, commit size)
- [ ] Repository health checker (unused branches, large files, etc.)

**Advanced Features**:

- [ ] GPG commit signing automation
- [ ] Automatic backup before dangerous operations
- [ ] Git alias library for common operations
- [ ] Integration with CI/CD (trigger builds on specific patterns)
- [ ] Metrics dashboard (commits per day, PR turnaround time, etc.)

**Deliverables**:

- [ ] Working framework with installation script
- [ ] Comprehensive documentation
- [ ] Test suite for all scripts
- [ ] Configuration system for team customization
- [ ] Demo video showing all features

### Example Hook: Pre-commit with Multiple Checks

```bash
#!/bin/bash
# .git/hooks/pre-commit

set -e

echo "🔍 Running pre-commit checks..."

# Check 1: No debug statements
echo "  - Checking for debug statements..."
if git diff --cached | grep -E "(console\.log|debugger|binding\.pry|pdb\.set_trace)"; then
    echo "❌ Error: Remove debug statements before committing"
    exit 1
fi

# Check 2: File size limit
echo "  - Checking file sizes..."
MAX_SIZE=5242880  # 5MB
for file in $(git diff --cached --name-only); do
    if [ -f "$file" ]; then
        size=$(wc -c < "$file")
        if [ $size -gt $MAX_SIZE ]; then
            echo "❌ Error: $file exceeds 5MB limit"
            exit 1
        fi
    fi
done

# Check 3: No secrets
echo "  - Checking for secrets..."
if git diff --cached | grep -E "(password|api_key|secret|token)\s*=\s*['\"][^'\"]+['\"]"; then
    echo "❌ Error: Possible hardcoded secret detected"
    exit 1
fi

# Check 4: Run linter
echo "  - Running linter..."
npm run lint --silent

# Check 5: Check imports
echo "  - Checking for unused imports..."
# Add your import checker here

echo "✅ All pre-commit checks passed!"
exit 0
```

### Evaluation Criteria

- **Functionality (40%)**: All tools work correctly and reliably
- **Code Quality (25%)**: Clean, maintainable, well-tested code
- **Usability (20%)**: Easy to install, configure, and use
- **Documentation (15%)**: Clear documentation with examples

---

## Project 2: Advanced Repository Management System

**Time**: 3-4 weeks  
**Difficulty**: ⭐⭐⭐ Advanced  
**Focus**: Complex multi-repo management

### Description

Build a system to manage multiple related repositories (microservices, monorepo, etc.) with synchronized operations, cross-repo analysis, and automated maintenance.

### Requirements

**Multi-Repo Management**:

- [ ] Initialize related repos with consistent structure
- [ ] Synchronize operations across repos (branch, commit, push)
- [ ] Manage interdependencies between repos
- [ ] Track versions and compatibility matrices
- [ ] Automated integration testing across repos

**Analysis Tools**:

- [ ] Cross-repo dependency analyzer
- [ ] Duplicate code detector across repositories
- [ ] Breaking change detector (API changes across services)
- [ ] Repository health metrics (commit frequency, PR stats, etc.)
- [ ] Technical debt tracker

**Automation**:

- [ ] Automated branch creation across related repos
- [ ] Synchronized releases with version bumping
- [ ] Automated migration scripts (run across all repos)
- [ ] Batch operations (cherry-pick, revert, etc.)
- [ ] Automated documentation generation

**Advanced Git Usage**:

- [ ] Submodule or subtree management
- [ ] Git worktrees for parallel testing
- [ ] Custom merge strategies for specific files
- [ ] Git LFS for shared assets
- [ ] Repository templates with Git hooks

**Deliverables**:

- [ ] Working CLI tool or web interface
- [ ] Support for at least 5 interconnected repos
- [ ] Comprehensive test suite
- [ ] Documentation with architecture diagrams
- [ ] Case study showing real-world usage

### Example: Multi-Repo Sync Script

```bash
#!/bin/bash
# sync-repos.sh - Synchronize operation across multiple repos

REPOS=(
    "services/auth"
    "services/api"
    "services/frontend"
    "services/worker"
)

OPERATION=$1
BRANCH=$2

case $OPERATION in
    "branch")
        echo "Creating branch '$BRANCH' in all repos..."
        for repo in "${REPOS[@]}"; do
            cd "$repo"
            git checkout main
            git pull
            git checkout -b "$BRANCH"
            cd - > /dev/null
            echo "✓ Created branch in $repo"
        done
        ;;
    
    "status")
        echo "Getting status of all repos..."
        for repo in "${REPOS[@]}"; do
            echo -e "\n=== $repo ==="
            cd "$repo"
            git status -sb
            cd - > /dev/null
        done
        ;;
    
    "sync")
        echo "Syncing all repos with main..."
        for repo in "${REPOS[@]}"; do
            cd "$repo"
            current_branch=$(git branch --show-current)
            git checkout main
            git pull
            git checkout "$current_branch"
            git merge main
            cd - > /dev/null
            echo "✓ Synced $repo"
        done
        ;;
    
    *)
        echo "Usage: $0 {branch|status|sync} [branch-name]"
        exit 1
        ;;
esac
```

### Evaluation Criteria

- **Architecture (35%)**: Well-designed, scalable system
- **Functionality (30%)**: Comprehensive feature set
- **Reliability (20%)**: Handles errors, edge cases gracefully
- **Documentation (15%)**: Clear docs with real-world examples

---

## Project 3: Git Internals Explorer

**Time**: 2-3 weeks  
**Difficulty**: ⭐⭐⭐ Advanced  
**Focus**: Deep understanding of Git internals

### Description

Build a tool that explores and visualizes Git internals, helping developers understand how Git works under the hood.

### Requirements

**Object Explorer**:

- [ ] List all Git objects (blobs, trees, commits, tags)
- [ ] Visualize object relationships
- [ ] Show object content and metadata
- [ ] Track object references
- [ ] Identify dangling and unreachable objects

**History Visualization**:

- [ ] Generate commit graph with branches
- [ ] Show merge patterns and strategies
- [ ] Visualize rebase operations
- [ ] Display reflog as timeline
- [ ] Show parent-child relationships

**Repository Analysis**:

- [ ] Repository size breakdown by type
- [ ] Identify largest objects
- [ ] Find duplicate content
- [ ] Analyze pack files
- [ ] Show repository structure (.git directory)

**Educational Features**:

- [ ] Interactive tutorial mode
- [ ] Step-by-step commit creation visualization
- [ ] Branching and merging animations
- [ ] Comparison of operations (merge vs rebase)
- [ ] Quiz mode to test understanding

**Advanced Features**:

- [ ] Recover deleted branches/commits
- [ ] Garbage collection simulation
- [ ] Pack file creation visualization
- [ ] Object compression analysis
- [ ] Delta compression explanation

**Deliverables**:

- [ ] Working application (CLI or GUI)
- [ ] Interactive visualizations
- [ ] Educational content/tutorials
- [ ] Documentation explaining Git internals
- [ ] Video demo of all features

### Example: Object Graph Visualizer

```bash
#!/bin/bash
# visualize-objects.sh

echo "Git Object Graph"
echo "=================="

# Get all commits
commits=$(git rev-list --all)

for commit in $commits; do
    # Get commit info
    tree=$(git cat-file -p $commit | grep "^tree" | cut -d' ' -f2)
    parents=$(git cat-file -p $commit | grep "^parent" | cut -d' ' -f2)
    
    echo ""
    echo "Commit: ${commit:0:8}"
    echo "├─ Tree: ${tree:0:8}"
    
    # Show tree contents
    git cat-file -p $tree | while read mode type hash name; do
        echo "│  ├─ $name ($type ${hash:0:8})"
        
        # If it's a tree, show one level deeper
        if [ "$type" = "tree" ]; then
            git cat-file -p $hash | while read m2 t2 h2 n2; do
                echo "│  │  ├─ $n2 ($t2 ${h2:0:8})"
            done
        fi
    done
    
    # Show parents
    if [ -n "$parents" ]; then
        for parent in $parents; do
            echo "└─ Parent: ${parent:0:8}"
        done
    fi
done
```

### Evaluation Criteria

- **Technical Depth (40%)**: Comprehensive coverage of Git internals
- **Visualization (30%)**: Clear, helpful visualizations
- **Educational Value (20%)**: Helps users learn Git internals
- **Code Quality (10%)**: Clean, maintainable implementation

---

## Project 4: Git-Based CI/CD Pipeline

**Time**: 3-4 weeks  
**Difficulty**: ⭐⭐⭐⭐ Expert  
**Focus**: Integration of Git with deployment workflows

### Description

Build a complete CI/CD pipeline that uses Git hooks and workflows to automate testing, building, and deployment.

### Requirements

**Pipeline Stages**:

- [ ] Commit stage: Lint, test, security scan
- [ ] Build stage: Compile, bundle, containerize
- [ ] Deploy stage: Deploy to staging/production
- [ ] Rollback mechanism using Git history
- [ ] Multi-environment support

**Git Integration**:

- [ ] Server-side hooks for automation
- [ ] Branch-based deployments (main→prod, dev→staging)
- [ ] Tag-based releases
- [ ] PR preview deployments
- [ ] Automatic version bumping

**Advanced Features**:

- [ ] Blue-green deployments
- [ ] Canary releases
- [ ] Automated rollback on failure
- [ ] Deployment analytics
- [ ] Notification system (Slack, email, etc.)

**Deliverables**:

- [ ] Complete working pipeline
- [ ] Documentation for setup and usage
- [ ] Example application deployed through pipeline
- [ ] Monitoring dashboard
- [ ] Post-mortem of a simulated incident

### Evaluation Criteria

- **Completeness (35%)**: Full CI/CD workflow implemented
- **Reliability (30%)**: Handles failures gracefully
- **Automation (20%)**: Minimal manual intervention required
- **Documentation (15%)**: Clear setup and operation guides

---

Choose one project that interests you most and demonstrates mastery of advanced Git concepts.
