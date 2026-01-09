# Git Operations Examples

Master Git workflows using `gh copilot suggest`.

## Basic Git Operations

### Status and Info

```bash
# Status
gh copilot suggest "show git status"
# → git status

# Detailed status
gh copilot suggest "show git status with detailed changes"
# → git status -vv

# Short status
gh copilot suggest "show concise git status"
# → git status -s

# Current branch
gh copilot suggest "show current branch name"
# → git branch --show-current
```

### Adding and Committing

```bash
# Add specific files
gh copilot suggest "add specific file to staging"
# → git add filename.txt

# Add all changes
gh copilot suggest "stage all modified files"
# → git add -A

# Add with patch mode
gh copilot suggest "interactively stage changes"
# → git add -p

# Commit with message
gh copilot suggest "commit staged changes with message"
# → git commit -m "Your message"

# Commit all tracked files
gh copilot suggest "commit all modified tracked files"
# → git commit -am "Your message"
```

## Branch Management

### Creating and Switching

```bash
# Create branch
gh copilot suggest "create new branch"
# → git branch feature-name

# Create and switch
gh copilot suggest "create and switch to new branch"
# → git checkout -b feature-name
# or → git switch -c feature-name

# Switch branch
gh copilot suggest "switch to existing branch"
# → git checkout main
# or → git switch main
```

### Listing and Viewing

```bash
# List local branches
gh copilot suggest "list all local branches"
# → git branch

# List remote branches
gh copilot suggest "list all remote branches"
# → git branch -r

# List all branches
gh copilot suggest "list both local and remote branches"
# → git branch -a

# Show merged branches
gh copilot suggest "show branches merged into main"
# → git branch --merged main
```

### Deleting Branches

```bash
# Delete local branch
gh copilot suggest "delete local branch"
# → git branch -d branch-name

# Force delete
gh copilot suggest "force delete unmerged branch"
# → git branch -D branch-name

# Delete remote branch
gh copilot suggest "delete branch from remote"
# → git push origin --delete branch-name

# Prune deleted remote branches
gh copilot suggest "remove local references to deleted remote branches"
# → git fetch --prune
```

### Bulk Branch Operations

```bash
# Delete all merged branches
gh copilot suggest "delete all local branches that have been merged"
# → git branch --merged | grep -v "\*" | xargs git branch -d

# List stale branches
gh copilot suggest "show branches not updated in 6 months"
# → git for-each-ref --sort=-committerdate refs/heads/ --format='%(committerdate:short) %(refname:short)' | awk '$1 < "'$(date -d '6 months ago' +%Y-%m-%d)'"'
```

## History and Logs

### Viewing History

```bash
# Recent commits
gh copilot suggest "show last 10 commits"
# → git log -10

# One line per commit
gh copilot suggest "show commit history in compact format"
# → git log --oneline

# With graph
gh copilot suggest "show branch graph with commits"
# → git log --graph --oneline --all

# Pretty format
gh copilot suggest "show detailed commit history"
# → git log --pretty=format:"%h - %an, %ar : %s"
```

### Searching History

```bash
# By author
gh copilot suggest "show commits by specific author"
# → git log --author="John Doe"

# By date
gh copilot suggest "show commits from last week"
# → git log --since="1 week ago"

# By message
gh copilot suggest "find commits with message containing bugfix"
# → git log --grep="bugfix"

# By file
gh copilot suggest "show commits that modified specific file"
# → git log -- path/to/file.js
```

### Commit Statistics

```bash
# Commits per author
gh copilot suggest "count commits by author"
# → git shortlog -sn

# Changed files
gh copilot suggest "show files changed in last commit"
# → git show --name-only

# Commit stats
gh copilot suggest "show statistics for commits"
# → git log --stat

# Activity by date
gh copilot suggest "show commit activity by date"
# → git log --pretty=format:"%ad" --date=short | sort | uniq -c
```

## Viewing Changes

### Diff Commands

```bash
# Unstaged changes
gh copilot suggest "show unstaged changes"
# → git diff

# Staged changes
gh copilot suggest "show changes that are staged"
# → git diff --cached

# Changes between branches
gh copilot suggest "compare two branches"
# → git diff main..feature-branch

# Changes in specific file
gh copilot suggest "show changes in specific file"
# → git diff filename.js

# Word-level diff
gh copilot suggest "show word by word diff"
# → git diff --word-diff
```

### Comparing

```bash
# Files changed between branches
gh copilot suggest "list files different between branches"
# → git diff --name-only main..feature

# Commits ahead/behind
gh copilot suggest "show how many commits ahead or behind"
# → git rev-list --left-right --count main...feature

# Show what changed in commit
gh copilot suggest "show changes in specific commit"
# → git show commit-hash
```

## Undoing Changes

### Unstaging

```bash
# Unstage file
gh copilot suggest "unstage a file"
# → git restore --staged filename

# Unstage all
gh copilot suggest "unstage all files"
# → git reset HEAD
```

### Discarding Changes

```bash
# Discard changes in file
gh copilot suggest "discard uncommitted changes in file"
# → git restore filename
# or → git checkout -- filename

# Discard all changes
gh copilot suggest "discard all uncommitted changes"
# → git restore .

# Clean untracked files
gh copilot suggest "remove untracked files"
# → git clean -fd
```

### Undoing Commits

```bash
# Undo last commit (keep changes)
gh copilot suggest "undo last commit but keep changes"
# → git reset --soft HEAD~1

# Undo last commit (discard changes)
gh copilot suggest "undo last commit and discard changes"
# → git reset --hard HEAD~1

# Amend last commit
gh copilot suggest "modify last commit"
# → git commit --amend

# Revert commit (create new commit)
gh copilot suggest "revert a specific commit"
# → git revert commit-hash
```

## Remote Operations

### Remote Management

```bash
# List remotes
gh copilot suggest "show remote repositories"
# → git remote -v

# Add remote
gh copilot suggest "add remote repository"
# → git remote add origin url

# Change remote URL
gh copilot suggest "update remote URL"
# → git remote set-url origin new-url

# Remove remote
gh copilot suggest "remove remote"
# → git remote remove origin
```

### Fetching and Pulling

```bash
# Fetch updates
gh copilot suggest "fetch updates from remote"
# → git fetch origin

# Pull changes
gh copilot suggest "pull latest changes from main"
# → git pull origin main

# Pull with rebase
gh copilot suggest "pull and rebase instead of merge"
# → git pull --rebase origin main

# Fetch all remotes
gh copilot suggest "fetch from all remotes"
# → git fetch --all
```

### Pushing

```bash
# Push to remote
gh copilot suggest "push commits to remote"
# → git push origin branch-name

# Push and set upstream
gh copilot suggest "push new branch to remote"
# → git push -u origin branch-name

# Force push (dangerous!)
gh copilot suggest "force push to remote"
# → git push --force origin branch-name

# Push tags
gh copilot suggest "push tags to remote"
# → git push --tags
```

## Stashing

```bash
# Stash changes
gh copilot suggest "save current changes temporarily"
# → git stash

# Stash with message
gh copilot suggest "stash changes with description"
# → git stash save "work in progress"

# List stashes
gh copilot suggest "list all stashes"
# → git stash list

# Apply stash
gh copilot suggest "apply most recent stash"
# → git stash apply

# Pop stash
gh copilot suggest "apply and remove most recent stash"
# → git stash pop

# Delete stash
gh copilot suggest "delete specific stash"
# → git stash drop stash@{0}
```

## Tagging

```bash
# Create tag
gh copilot suggest "create annotated tag"
# → git tag -a v1.0.0 -m "Version 1.0.0"

# List tags
gh copilot suggest "list all tags"
# → git tag

# Show tag info
gh copilot suggest "show tag details"
# → git show v1.0.0

# Delete tag
gh copilot suggest "delete local tag"
# → git tag -d v1.0.0

# Delete remote tag
gh copilot suggest "delete tag from remote"
# → git push origin --delete v1.0.0
```

## Advanced Operations

### Rebasing

```bash
# Rebase onto main
gh copilot suggest "rebase current branch onto main"
# → git rebase main

# Interactive rebase
gh copilot suggest "interactively rebase last 5 commits"
# → git rebase -i HEAD~5

# Continue after resolving conflicts
gh copilot suggest "continue rebase after fixing conflicts"
# → git rebase --continue

# Abort rebase
gh copilot suggest "cancel ongoing rebase"
# → git rebase --abort
```

### Cherry-picking

```bash
# Cherry-pick commit
gh copilot suggest "apply specific commit to current branch"
# → git cherry-pick commit-hash

# Cherry-pick multiple commits
gh copilot suggest "cherry-pick range of commits"
# → git cherry-pick commit1..commit2

# Continue after conflict
gh copilot suggest "continue cherry-pick after resolving conflicts"
# → git cherry-pick --continue
```

### Submodules

```bash
# Add submodule
gh copilot suggest "add git submodule"
# → git submodule add url path

# Update submodules
gh copilot suggest "update all submodules"
# → git submodule update --init --recursive

# Clone with submodules
gh copilot suggest "clone repository with submodules"
# → git clone --recursive url
```

## Configuration

```bash
# Set username
gh copilot suggest "configure git username"
# → git config --global user.name "Your Name"

# Set email
gh copilot suggest "configure git email"
# → git config --global user.email "email@example.com"

# Set default editor
gh copilot suggest "set vim as default git editor"
# → git config --global core.editor vim

# List all config
gh copilot suggest "show all git configuration"
# → git config --list

# Set alias
gh copilot suggest "create git alias for status"
# → git config --global alias.st status
```

## Cleanup and Maintenance

```bash
# Garbage collection
gh copilot suggest "optimize git repository"
# → git gc

# Clean up
gh copilot suggest "remove unreachable objects"
# → git prune

# Check integrity
gh copilot suggest "verify git repository integrity"
# → git fsck

# Repository size
gh copilot suggest "show repository size"
# → git count-objects -vH
```

## Practical Workflows

### Feature Branch Workflow

```bash
# 1. Create feature branch
gh copilot suggest "create feature branch from main"

# 2. Work and commit
gh copilot suggest "commit changes to feature branch"

# 3. Update from main
gh copilot suggest "merge latest main into feature branch"

# 4. Push feature
gh copilot suggest "push feature branch to remote"

# 5. After PR merge, cleanup
gh copilot suggest "delete merged feature branch locally and remotely"
```

### Fix Merge Conflicts

```bash
# 1. Attempt merge
gh copilot suggest "merge main into current branch"

# 2. Show conflicts
gh copilot suggest "show files with merge conflicts"
# → git diff --name-only --diff-filter=U

# 3. After resolving manually
gh copilot suggest "mark conflicts as resolved and continue"
# → git add resolved-file.js && git commit
```

### Bisect to Find Bug

```bash
# 1. Start bisect
gh copilot suggest "start git bisect session"
# → git bisect start

# 2. Mark bad commit
gh copilot suggest "mark current commit as bad"
# → git bisect bad

# 3. Mark good commit
gh copilot suggest "mark specific commit as good"
# → git bisect good commit-hash

# 4. After finding bad commit
gh copilot suggest "end bisect session"
# → git bisect reset
```

## Tips

1. **Always check status first**: Before complex operations
2. **Create backup branch**: Before rebasing or resetting
3. **Commit often**: Small, focused commits are better
4. **Write good messages**: Clear, descriptive commit messages
5. **Pull before push**: Avoid conflicts by staying updated

---

**Related**: [file-operations.md](./file-operations.md) | [docker-k8s.md](./docker-k8s.md)
