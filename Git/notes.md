# Git Basics

Git is a distributed version control system. It tracks changes to files over time (usually code), allowing multiple people to work on the same project without overwriting each other's work.

Every developer has a full copy of the project's history locally, so most operations such as commits, history, and branching work offline. Only operations such as pushing and pulling communicate with a remote server like GitHub, GitLab, or Bitbucket.

## Core Concepts

* **Repository (repo)** — The project folder tracked by Git, containing the full history.
* **Commit** — A saved snapshot of changes, with a message describing what changed.
* **Branch** — An independent line of development, allowing you to work on features without affecting the main codebase.
* **Merge** — Combining changes from one branch into another.
* **Remote** — A hosted version of the repository (for example, on GitHub) that you push to and pull from.
* **Working directory** — Where you make changes to your files.
* **Staging area** — Where you prepare changes before committing them.
* **Repository** — Where Git stores committed changes.

The basic flow is:

```text
Edited files → Staging area → Commit
             git add       git commit
```

# Basic Git Commands

## Setup

```bash
git config --global user.name "Your Name"
git config --global user.email "you@example.com"

git init
# Initialize a new repository in the current folder

git clone <repository-url>
# Copy an existing remote repository locally
```

## Basic Workflow

```bash
git status
# See what's changed or staged

git add <file>
# Stage a specific file

git add .
# Stage all changed files

git commit -m "message"
# Save staged changes as a commit

git log
# View commit history

git diff
# See unstaged changes

git diff --staged
# See staged changes that are not yet committed
```

## Branching

```bash
git branch
# List branches

git branch <branch-name>
# Create a new branch

git checkout <branch-name>
# Switch to a branch

git checkout -b <branch-name>
# Create and switch to a new branch

git switch <branch-name>
# Modern alternative to git checkout

git merge <branch-name>
# Merge another branch into the current branch

git branch -d <branch-name>
# Delete a branch
```

## Remote / Syncing

```bash
git remote -v
# List remote repositories

git remote add origin <repository-url>
# Link a remote repository

git push origin <branch-name>
# Push local commits to the remote repository

git pull origin <branch-name>
# Fetch and merge remote changes

git fetch
# Download remote changes without merging them
```

## Undoing Changes

```bash
git restore <file>
# Discard unstaged changes to a file

git reset <file>
# Unstage a file while keeping the changes

git reset --hard
# Discard all changes back to a commit (destructive)

git revert <commit>
# Create a new commit that undoes a previous commit
# This is safer for shared history
```

## Other Useful Commands

```bash
git stash
# Temporarily shelve uncommitted changes

git stash pop
# Reapply stashed changes

git rebase <branch-name>
# Replay commits on top of another branch

git tag <tag-name>
# Mark a specific commit, such as a release
```

## Quick Git Workflow

A typical workflow looks like this:

```bash
git status
git add .
git commit -m "Add new feature"
git push origin main
```

This means:

1. Check the current status.
2. Stage your changes.
3. Commit the changes.
4. Push the commit to the remote repository.
