---
tags:
  - git
howto: false
title: GIT Cheat Sheet
description: A quick reference guide for essential Git commands.
---

# GIT Cheat Sheet

### Setup

- Set user details

```bash
git config --global user.name "Your Name"
```

```bash
git config --global user.email "your.email@example.com"
```

- Check config

```bash
git config --list
```

### Creating and Cloning Repositories

- Initialize a new Git repository

```bash
git init
```

- Clone an existing repository

```bash
git clone <repository-url>
```

### Basic Commands

- Check the status of the working directory

```bash
git status
```

- Add files to staging area

1. Add specific file

```bash
git add <file>
```

2. Add all files

```bash
git add .
```

- Commit changes

```bash
git commit -m "Commit message"
```

### Branching and Merging

- List branches

```bash
git branch
```

- Create a new branch

```bash
git branch <branch-name>
```

- Switch to a branch

```bash
git checkout <branch-name>
```

- Create and switch to a new branch

```bash
git checkout -b <branch-name>
```

- Merge a branch into the current branch

```bash
git merge <branch-name>
```

### Remote Repositories

- Add a remote repository

```bash
git remote add origin <repository-url>
```

- Push changes to remote

```bash
git push origin <branch-name>
```

- Pull latest changes from remote

```bash
git pull origin <branch-name>
```

### Undoing Changes

- Unstage a file

```bash
git reset HEAD <file>
```

- Discard local changes

```bash
git checkout -- <file>
```

- Revert a commit

```bash
git revert <commit-hash>
```

### Log and History

- Show commit history

```bash
git log
```

- Show commit history in one line

```bash
git log --oneline
```

### Stashing

## Save uncommitted changes

```bash
git stash
```

- Apply the latest stashed changes

```bash
git stash pop
```

### Tags

- List all tags

```bash
git tag
```

- Create a new tag

```bash
git tag -a v1.0 -m "Version 1.0"
```

- Push tags to remote

```bash
git push origin --tags
```

### Submodules

- Add a submodule

```bash
git submodule add <repository-url> <path>
```

- Initialize submodules

```bash
git submodule update --init --recursive
```

### Advanced Commands

- Squash commits during interactive rebase

```bash
git rebase -i HEAD~<number-of-commits>
```

- Amend the last commit message

```bash
git commit --amend -m "New commit message"
```

- Hard reset to a specific commit

```bash
git reset --hard <commit-hash>
```

This cheat sheet provides a quick reference to essential Git commands for everyday development.
