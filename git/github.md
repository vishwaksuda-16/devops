# 🐙 Git & GitHub Beginner's Guide

A beginner-friendly guide covering Git installation and essential commands for getting started.

---

## Table of Contents

1. [Installation](#-installation)
2. [Initial Setup](#-initial-setup)
3. [Basic Commands](#-basic-commands)
4. [Working with Files](#-working-with-files)
5. [Branching Basics](#-branching-basics)
6. [GitHub Integration](#-github-integration)
7. [Common Workflows](#-common-workflows)
8. [Troubleshooting](#-troubleshooting)

---

## 🔧 Installation

### Windows
1. **Download Git:**
   - Go to: https://git-scm.com/download/win
   - Download and run the installer
   - Use default settings (recommended for beginners)

2. **Verify Installation:**
   ```bash
   git --version
   ```

### Linux (Ubuntu/Debian)
```bash
sudo apt update
sudo apt install git -y
git --version
```

### macOS
```bash
# Install using Homebrew (if available)
brew install git

# Or install Xcode Command Line Tools
xcode-select --install
```

---

## ⚙️ Initial Setup

### Configure Your Identity
```bash
git config --global user.name "Your Name"
git config --global user.email "your.email@gmail.com"
```

### Check Your Settings
```bash
git config --list
git config user.name
git config user.email
```

---

## 🔨 Basic Commands

### Starting a Repository

**Option 1: Create New Repository**
```bash
mkdir my-project
cd my-project
git init
```

**Option 2: Clone Existing Repository**
```bash
git clone https://github.com/username/repository-name.git
cd repository-name
```

### Check Status
```bash
git status                    # see what's changed
```

---

## 📄 Working with Files

### Adding Files
```bash
git add filename.txt          # add specific file
git add .                     # add all files
git add *.txt                 # add all .txt files
```

### Committing Changes
```bash
git commit -m "Your message here"
git commit -am "Add and commit in one step"    # for tracked files only
```

### Viewing Changes
```bash
git diff                      # see unstaged changes
git diff --staged             # see staged changes
git log                       # see commit history
git log --oneline             # compact history
```

---

## 🌿 Branching Basics

### Working with Branches
```bash
git branch                    # list all branches
git branch new-branch-name    # create new branch
git checkout branch-name      # switch to branch
git checkout -b new-branch    # create and switch to new branch
git branch -d branch-name     # delete branch
```

### Merging
```bash
git checkout main             # switch to main branch
git merge feature-branch      # merge feature-branch into main
```

---

## 🐙 GitHub Integration

### Connecting to GitHub

**Step 1: Create Repository on GitHub**
- Go to github.com
- Click "New repository"
- Give it a name
- Don't initialize with README (if you already have local files)

**Step 2: Connect Local Repository**
```bash
git remote add origin https://github.com/username/repository-name.git
git remote -v                 # verify remote connection
```

### Pushing and Pulling
```bash
git push origin main          # push to GitHub
git push -u origin main       # push and set upstream (first time)
git pull origin main          # get latest changes from GitHub
git pull                      # pull from default remote/branch
```

### Basic GitHub Workflow
```bash
# 1. Make changes to files
echo "Hello World" > README.md

# 2. Add changes
git add README.md

# 3. Commit changes
git commit -m "Add README file"

# 4. Push to GitHub
git push origin main
```

---

## 🔄 Common Workflows

### Daily Git Workflow
```bash
# 1. Check current status
git status

# 2. Pull latest changes (if working with others)
git pull

# 3. Make your changes to files
# ... edit files ...

# 4. Add changes
git add .

# 5. Commit with message
git commit -m "Describe what you changed"

# 6. Push to GitHub
git push
```

### Working on New Feature
```bash
# 1. Create new branch
git checkout -b new-feature

# 2. Make changes and commit
git add .
git commit -m "Add new feature"

# 3. Push new branch
git push origin new-feature

# 4. Switch back to main
git checkout main

# 5. Merge feature (after testing)
git merge new-feature

# 6. Push updated main
git push origin main

# 7. Delete feature branch (optional)
git branch -d new-feature
```

---

## 🔧 Troubleshooting

### Common Issues and Solutions

**Problem: "Repository not found"**
```bash
# Check remote URL
git remote -v
# Fix URL if wrong
git remote set-url origin https://github.com/username/correct-repo.git
```

**Problem: Merge conflicts**
```bash
# 1. Open conflicted files and edit them
# 2. Remove conflict markers (<<<<, ====, >>>>)
# 3. Add resolved files
git add filename.txt
# 4. Commit the merge
git commit -m "Resolve merge conflict"
```

**Problem: Want to undo last commit**
```bash
git reset --soft HEAD~1       # undo commit but keep changes staged
git reset --hard HEAD~1       # undo commit and discard changes (careful!)
```

**Problem: Want to discard local changes**
```bash
git checkout -- filename.txt  # discard changes to specific file
git checkout .                # discard all local changes (careful!)
```

**Problem: Authentication issues with GitHub**
```bash
# Use personal access token instead of password
# GitHub Settings → Developer settings → Personal access tokens
# Use token as password when prompted
```

---

## 📝 Essential Commands Summary

### Repository Setup
```bash
git init                      # start new repository
git clone <url>               # copy repository from GitHub
git config --global user.name "Name"
git config --global user.email "email"
```

### Daily Commands
```bash
git status                    # check what's changed
git add <file>                # stage file for commit
git add .                     # stage all files
git commit -m "message"       # save changes with message
git push                      # upload to GitHub
git pull                      # download from GitHub
```

### Branch Commands
```bash
git branch                    # list branches
git checkout <branch>         # switch branch
git checkout -b <branch>      # create and switch to new branch
git merge <branch>            # merge branch into current branch
```

### Remote Commands
```bash
git remote add origin <url>   # connect to GitHub repository
git remote -v                 # show remote connections
git push origin main          # push to specific branch
git pull origin main          # pull from specific branch
```

### Information Commands
```bash
git log                       # see commit history
git log --oneline            # compact history
git diff                     # see unstaged changes
git diff --staged            # see staged changes
```

---

## 🎯 Quick Start Checklist

**Setting up your first repository:**

1. ✅ Install Git
2. ✅ Configure name and email
3. ✅ Create/clone repository
4. ✅ Make some changes
5. ✅ Add and commit changes
6. ✅ Push to GitHub

**Basic commands to remember:**
- `git status` (check what's happening)
- `git add .` (stage all changes)  
- `git commit -m "message"` (save changes)
- `git push` (upload to GitHub)
- `git pull` (download from GitHub)

---
