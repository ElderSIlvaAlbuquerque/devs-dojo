# Getting Started with Git Style School

## Prerequisites

- None! Git is for everyone, from day one.

## Installation

### Linux (Ubuntu/Debian)

```bash
sudo apt update
sudo apt install git
```

### Linux (Fedora/RHEL)

```bash
sudo dnf install git
```

### macOS

```bash
brew install git
```

### Windows

Download from: https://git-scm.com/download/win

## Initial Configuration

After installation, configure your identity:

```bash
# Set your name
git config --global user.name "Your Name"

# Set your email
git config --global user.email "your@email.com"

# Set default branch name
git config --global init.defaultBranch main

# Set default editor (optional)
git config --global core.editor "code --wait"  # VS Code
# or
git config --global core.editor "vim"  # Vim

# Enable color output
git config --global color.ui auto
```

## Verify Installation

```bash
git --version
# Should output: git version 2.x.x

git config --list
# Should show your configurations
```

## Setup GitHub/GitLab Account

1. Create account at https://github.com or https://gitlab.com
2. Generate SSH key:
   ```bash
   ssh-keygen -t ed25519 -C "your@email.com"
   ```
3. Add SSH key to GitHub:
   ```bash
   cat ~/.ssh/id_ed25519.pub
   # Copy output and add to GitHub → Settings → SSH Keys
   ```
4. Test connection:
   ```bash
   ssh -T git@github.com
   # Should see: "Hi username! You've successfully authenticated"
   ```

## Your First Repository

```bash
# Create a directory
mkdir my-first-repo
cd my-first-repo

# Initialize Git
git init

# Create a file
echo "# My First Repo" > README.md

# Stage the file
git add README.md

# Commit
git commit -m "Initial commit"

# View history
git log
```

## Next Steps

Start with [White Belt - Lesson 1: Git Basics](02-white-belt/lessons.md)
