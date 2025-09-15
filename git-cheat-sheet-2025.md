# Git Cheat Sheet - Quick Reference Guide

## Essential Setup Commands

```bash
# Initial Git configuration
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
git config --global init.defaultBranch main
git config --global color.ui auto

# Set VS Code as default editor
git config --global core.editor "code --wait"

# View all configuration
git config --list
```

## Repository Operations

### Starting a Repository
```bash
git init                              # Initialize new repository
git init --initial-branch=main        # Initialize with specific branch
git clone <url>                       # Clone remote repository
git clone -b <branch> <url>           # Clone specific branch
```

### Basic Workflow
```bash
git status                            # Check repository status
git add <file>                        # Stage specific file
git add .                            # Stage all changes
git add --all                        # Stage all changes (including deletions)
git commit -m "message"              # Commit with message
git commit -am "message"             # Stage and commit tracked files
git push origin main                 # Push to remote
git pull origin main                 # Pull from remote
```

## Modern Commit Messages (Conventional Commits)

```bash
git commit -m "feat: add new feature"          # New feature
git commit -m "fix: resolve bug"              # Bug fix
git commit -m "docs: update README"           # Documentation
git commit -m "style: format code"            # Code formatting
git commit -m "refactor: improve structure"   # Code refactoring
git commit -m "test: add unit tests"          # Testing
git commit -m "chore: update dependencies"    # Maintenance
git commit -m "perf: optimize performance"    # Performance
git commit -m "ci: update workflow"           # CI/CD changes
git commit -m "build: update build config"    # Build system
git commit -m "revert: undo previous change"  # Revert commit
```

## Branch Management

### Basic Branching
```bash
git branch                           # List branches
git branch <name>                    # Create branch
git checkout <name>                  # Switch to branch
git checkout -b <name>               # Create and switch
git switch <name>                    # Modern switch command
git switch -c <name>                 # Modern create and switch
git branch -d <name>                 # Delete merged branch
git branch -D <name>                 # Force delete branch
```

### Branch Naming Conventions
```bash
feature/user-authentication          # New features
bugfix/login-validation             # Bug fixes
hotfix/security-patch               # Urgent fixes
experiment/new-architecture         # Experimental work
release/v1.2.0                      # Release preparation
```

### Merging and Rebasing
```bash
git merge <branch>                   # Merge branch
git merge --no-ff <branch>           # Force merge commit
git rebase <branch>                  # Rebase onto branch
git rebase -i HEAD~3                 # Interactive rebase
git cherry-pick <commit>             # Apply specific commit
```

## Remote Repository Management

### Remote Operations
```bash
git remote -v                        # List remotes
git remote add origin <url>          # Add remote
git remote set-url origin <url>      # Change remote URL
git remote remove <name>             # Remove remote

git fetch origin                     # Fetch from remote
git push origin <branch>             # Push branch
git push -u origin <branch>          # Push and set upstream
git push --force-with-lease          # Safe force push
git pull --rebase origin main        # Pull with rebase
```

## Viewing History and Changes

### Log and History
```bash
git log                              # View commit history
git log --oneline                    # Compact log view
git log --graph --oneline --all      # Visual branch history
git log --author="Name"              # Filter by author
git log --since="2 weeks ago"        # Filter by date
git log -p                           # Show patch/changes
git log --stat                       # Show file statistics
```

### Examining Changes
```bash
git diff                             # View unstaged changes
git diff --staged                    # View staged changes
git diff HEAD~1                      # Compare with previous commit
git diff <commit1> <commit2>         # Compare commits
git diff <branch1> <branch2>         # Compare branches
git show <commit>                    # Show commit details
```

## Stashing and Temporary Storage

```bash
git stash                            # Stash current changes
git stash save "message"             # Stash with message
git stash list                       # List all stashes
git stash pop                        # Apply and remove latest stash
git stash apply                      # Apply stash without removing
git stash apply stash@{2}            # Apply specific stash
git stash drop stash@{1}             # Delete specific stash
git stash clear                      # Delete all stashes
```

## Undoing Changes

### Working Directory and Staging
```bash
git checkout -- <file>               # Discard unstaged changes
git restore <file>                   # Modern discard changes
git reset HEAD <file>                # Unstage file
git restore --staged <file>          # Modern unstage file
git clean -fd                        # Remove untracked files/dirs
```

### Commit Level Undoing
```bash
git reset --soft HEAD~1              # Undo commit, keep changes staged
git reset HEAD~1                     # Undo commit, unstage changes
git reset --hard HEAD~1              # Undo commit, discard changes
git revert <commit>                  # Create new commit that undoes changes
git commit --amend                   # Modify last commit
```

## Advanced Operations

### File Operations
```bash
git rm <file>                        # Remove file from Git and filesystem
git rm --cached <file>               # Remove from Git, keep locally
git mv <old> <new>                   # Move/rename file
```

### Repository Maintenance
```bash
git gc                               # Garbage collection
git gc --aggressive                  # Aggressive cleanup
git fsck                             # Check repository integrity
git count-objects -v                 # Repository statistics
git remote prune origin              # Clean remote references
```

### Advanced History Manipulation
```bash
git reflog                           # View reference log
git reset --hard HEAD@{2}            # Reset using reflog
git filter-branch                    # Rewrite history (use carefully)
git blame <file>                     # Show line-by-line authorship
git bisect start                     # Start binary search for bugs
```

## Tags and Releases

```bash
git tag                              # List tags
git tag <name>                       # Create lightweight tag
git tag -a <name> -m "message"       # Create annotated tag
git tag -d <name>                    # Delete local tag
git push origin <tag>                # Push specific tag
git push origin --tags               # Push all tags
git push origin --delete <tag>       # Delete remote tag
```

## Git Configuration Tips

### Useful Aliases
```bash
git config --global alias.st status
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.cm commit
git config --global alias.lg "log --graph --oneline --all"
git config --global alias.unstage "reset HEAD --"
git config --global alias.last "log -1 HEAD"
```

### Performance Settings
```bash
git config --global core.preloadindex true
git config --global core.fscache true
git config --global gc.auto 256
```

## .gitignore Patterns

### Common Patterns
```gitignore
# Dependencies
node_modules/
*.log

# Build outputs
dist/
build/
*.exe
*.dll

# Environment files
.env
.env.local
.env.*.local

# IDE files
.vscode/
.idea/
*.swp
*.swo

# OS files
.DS_Store
Thumbs.db

# Language specific
__pycache__/
*.pyc
*.class
*.o
```

## Pre-commit Hooks Setup

### Install pre-commit framework
```bash
pip install pre-commit
pre-commit install
```

### Sample .pre-commit-config.yaml
```yaml
repos:
  - repo: https://github.com/pre-commit/pre-commit-hooks
    rev: v4.4.0
    hooks:
      - id: trailing-whitespace
      - id: end-of-file-fixer
      - id: check-yaml
      - id: check-merge-conflict
```

## Emergency Commands

### When Things Go Wrong
```bash
git reflog                           # Find lost commits
git reset --hard HEAD@{1}           # Recover from reflog
git fsck --lost-found               # Find dangling commits
git merge --abort                   # Abort failed merge
git rebase --abort                  # Abort failed rebase
git cherry-pick --abort             # Abort failed cherry-pick
```

### Conflict Resolution
```bash
git status                          # See conflicted files
# Edit files manually or use merge tool
git add <resolved-files>            # Mark as resolved
git commit                          # Complete merge
# Or use:
git mergetool                       # Open configured merge tool
```

## Modern Workflows

### GitHub Flow
1. Create feature branch from main
2. Make changes and commit
3. Push and create pull request
4. Review and merge to main
5. Delete feature branch

### Feature Branch Workflow
```bash
git checkout main
git pull origin main
git checkout -b feature/new-feature
# Make changes
git add .
git commit -m "feat: implement new feature"
git push -u origin feature/new-feature
# Create pull request
# After merge:
git checkout main
git pull origin main
git branch -d feature/new-feature
```

## VS Code Git Integration

### Useful Shortcuts
- `Ctrl+Shift+G`: Open Source Control panel
- `Ctrl+Enter`: Commit staged changes
- `Ctrl+Shift+P`: Command palette (type "Git:")
- `F1`: Show Git commands

### Extensions
- GitLens: Enhanced Git capabilities
- Git Graph: Visual commit graph
- Git History: File history viewer

---

## Quick Reference Summary

| Command | Description |
|---------|-------------|
| `git init` | Initialize repository |
| `git clone <url>` | Clone repository |
| `git add .` | Stage all changes |
| `git commit -m "msg"` | Commit with message |
| `git push origin main` | Push to remote |
| `git pull origin main` | Pull from remote |
| `git checkout -b <branch>` | Create and switch branch |
| `git merge <branch>` | Merge branch |
| `git status` | Check status |
| `git log --oneline` | View commit history |
| `git diff` | View changes |
| `git stash` | Temporarily save changes |

**Remember**: When in doubt, use `git status` to understand the current state of your repository!