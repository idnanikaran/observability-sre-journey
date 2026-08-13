Git is a distributed version control system — it tracks changes to files over time (usually code), letting multiple people work on the same project without overwriting each other's work. Every developer has a full copy of the project's history locally, so most operations (commits, history, branching) work offline, and only pushing/pulling talks to a remote server (like GitHub, GitLab, Bitbucket).

Core concepts:

Repository (repo) — the project folder tracked by Git, containing the full history.
Commit — a saved snapshot of changes, with a message describing what changed.
Branch — an independent line of development, so you can work on features without affecting the main codebase.
Merge — combining changes from one branch into another.
Remote — a hosted version of the repo (e.g., on GitHub) that you push to / pull from.
Working directory vs. staging area vs. repository — three states a change passes through: edited files → staged (git add) → committed (git commit).


Basic Git Commands

Setup

git config --global user.name "Your Name"
git config --global user.email "you@example.com"
git init                      # initialize a new repo in current folder
git clone <url>                # copy an existing remote repo locally

Basic workflow

git status                     # see what's changed / staged
git add <file>                 # stage a specific file
git add .                      # stage all changed files
git commit -m "message"        # save staged changes as a commit
git log                        # view commit history
git diff                       # see unstaged changes
git diff --staged              # see staged changes not yet committed

Branching

git branch                     # list branches
git branch <name>               # create a new branch
git checkout <name>             # switch to a branch
git checkout -b <name>          # create + switch in one step
git switch <name>               # modern alternative to checkout
git merge <branch>               # merge another branch into current one
git branch -d <name>             # delete a branch

Remote / syncing

git remote -v                   # list remotes
git remote add origin <url>     # link a remote repo
git push origin <branch>        # push local commits to remote
git pull origin <branch>        # fetch + merge remote changes
git fetch                       # download remote changes without merging

Undoing things

git restore <file>              # discard unstaged changes to a file
git reset <file>                # unstage a file (keep changes)
git reset --hard <commit>       # discard all changes back to a commit (destructive)
git revert <commit>              # create a new commit that undoes a previous one (safe for shared history)

Other useful ones

git stash                       # temporarily shelve uncommitted changes
git stash pop                   # reapply stashed changes
git rebase <branch>              # replay commits on top of another branch
git tag <name>                   # mark a specific commit (e.g., a release)

