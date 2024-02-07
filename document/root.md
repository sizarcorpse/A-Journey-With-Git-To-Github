# A Journey With Git To GitHub

[👨‍🎓 sizar corpse](https://github.com/sizarcorpse)

This document covers every basic command you need to do the vast majority of the things you’ll eventually spend your time doing with Git. By the end of the document, you should be able to configure and initialize a repository, begin and stop tracking files, and stage and commit changes.This document also show you how to set up Git to ignore certain files and file patterns, how to undo mistakes quickly and easily, how to browse the history of your project and view changes between commits, and how to push and pull from remote repositories.

<!-- table of content -->

## 📖 Table of Contents

- [A Journey With Git To GitHub](#a-journey-with-git-to-github)
  - [📖 Table of Contents](#-table-of-contents)
  - [Git Configuration](#git-configuration)
  - [Initializing a Repository](#initializing-a-repository)
  - [Creating Snapshots and Staging](#creating-snapshots-and-staging)
  - [Git Ignore](#git-ignore)
  - [Committing Staged](#committing-staged)
  - [Browsing Commit History](#browsing-commit-history)
  - [Diff whats changes on before commit (staged or un-staged)](#diff-whats-changes-on-before-commit-staged-or-un-staged)
  - [Remove, Move \& Rename files](#remove-move--rename-files)
  - [Revert \& Reset files from the staging area](#revert--reset-files-from-the-staging-area)
  - [Stash staging](#stash-staging)
  - [**`git branch`**](#git-branch)
    - [🎎 Merge branch](#-merge-branch)
    - [🤖 Remote Branch: Tracking, Deleting, Renaming](#-remote-branch-tracking-deleting-renaming)
  - [Remote Repositories](#remote-repositories)
  - [Push Repositories](#push-repositories)
  - [Pull](#pull)
  - [Fetch Repositories](#fetch-repositories)
  - [Update Remote](#update-remote)
  - [Git Rebase](#git-rebase)
  - [Git Tag](#git-tag)

## Git Configuration

```bash
# View all of settings
git config -list --show-origin

# Check git configuration
git config --list
git config -l

# Set git configuration
# Set global configuration

# Set name
git config --global users.name "<name>"

# Get name
git config users.name

# Set email
git config --global users.email "<email>"

# Get email
git config users.email

# Cache credentials
git config --global credential.helper cache
```

```bash
# Set global editor
git config --global core.editor "code --wait"
gti config --global core.editor "code-insiders --wait"

# Edit global settings with default editor
git config --global --edit
git config --global -e

# Enable autocrlf

# Windows
git config --global core.autocrlf true

# Mac
git config --global core.autocrlf input
```

```bash
# Set Diff Tools
git config --global diff.tool vscode
git config --global diff.toolvscode.cmd "code-insiders --wait --diff $LOCAL $REMOTE"
# Note: after setup difftool, use "git difftool" instead of "git diff"
```

```bash
# Set Default Branch Name for
git config --global init.defaultBranch main
```

## Initializing a Repository

```bash
# Initializing an existing directory as a Git repository
git init


# Clone/Retrieve an entire existing repository from via URL
git clone <url>

# With desire name
git clone <url> <name>
# Note:That command does the same thing as the previous one, but the target directory is called <name>.

# With desire remote name
git clone -o <name>

#Both desire remote name and directory name
git clone -o <name> <url> <name>
# Ex:git clone -o '<remote-name>' https://github.com/<author>/welcome-to-github <directory-name>
```

## Creating Snapshots and Staging

```bash

# Show the status of the current repository including staged, unstated, and untracked files
git status


# Show the status of the current repository including staged, unstated, and untracked files
git status -s
# ?? = untracked files, M = modified files, A = added files, D = deleted files, R = renamed files, C = copied files, U = updated files, ! = ignored files

# Add all files and folders recursively to the staging area
git add .

# Add single file to the staging area
git add <file>

# Add multiple files to the staging area
git add <file> <file>

# Add all files with a specific extension to the staging area
git add *.txt
```

## Git Ignore

```bash
# Create a .gitignore file
.gitignore

# Examine the contents of the .gitignore file
# #ignore all .a files
# *.a

# #but do track lib.a, even though you're ignoring .a files above
# !lib.a

# #only ignore the TODO file in the current directory, not subdir/TODO
# /TODO

# #ignore all files in any directory named build
# build/

# #ignore doc/notes.txt, but not doc/server/arch.txt
# doc/*.txt

# #ignore all .pdf files in the doc/ directory and any of its subdirectories
# doc/**/*.pdf
```

## Committing Staged

```bash

# Commit all staged files with long commit message
git commit

# Commit and show the Diff of your change
git commit -v

# Commit all staged files with a specific message
git commit -m "Initial commit"

# Commit all staged files without staging
git commit -a -m "Initial commit"
git commit -am "Initial commit"

# Show a specific commit
git show commit-id
git show HEAD~1

# Commit stage interactively / partially
git commit -p
```

## Browsing Commit History

```bash
# Show commit history of the current repository(current branch)
git log

# Show commit history of the current repository(all branches)
git log --all

# Show commit history including all files and their changes
git log -p

# Show commit history by one line
git log --oneline
git log --oneline --decorate

# Reverse order
git log --reverse

# With reflog
git --reflog

# Show commit history with a specific number of commits
git log -n 5
git log 5
#Note: Shows the last 5 commits

# Show some statistics about the changes in each commit.
git log --stat

# Show commit log as a graph
git log --graph
# One line
git log --graph --oneline
# All
git log --all --graph --oneline
```

```bash
# git log

# -p = show changes in each commit
# -n = show n commits
# --stat = show statistics about the changes in each commit
# --graph = show commit log as a graph
# --oneline = show commit log as one line
# --reverse = reverse order
# --shortstat = only the changed/insertions/deletions line from the --stat command
# --name-only = only show the names of the files that were changed
# --name-status = show the names of the files that were changed and their status
# --decorate = show commit log with colors and other decorations


# Git log Limiting the output

# -n = show n commits
# --since, --after = show commits after the date
# --until, --before = show commits before the date
# --author = show commits by the author
# --committer = show commits by the committer
# --grep = show commits that match the pattern
# -S = show the search pattern in the commit message
# Ex : git log --pretty="%h - %s" --author='<author>' --since="2021-10-01" --before="2022-11-01"
```

```bash
# Using Pretty
git log --pretty=oneline

# Using Pretty Format
git log --pretty=format:"%h %an %s"
git log --pretty="%h %an %s"

# %H  = Commit hash
# %h  = Abbreviated commit hash
# %T  = Tree hash
# %t  = Abbreviated tree hash
# %P  = Parent hashes
# %p  = Abbreviated parent hashes
# %an = Author name
# %ae = Author email
# %ad = Author date (format respects the --date=option)
# %ar = Author date, relative
# %cn = Committer name
# %ce = Committer email
# %cd = Committer date
# %cr = Committer date, relative
# %s  = Subject

# Using Pretty and Graph
git log --pretty=format:"%h %an %s" --graph
```

## Diff whats changes on before commit (staged or un-staged)

```bash
# Show changes on before commit(un-staged)
git diff
# Note: difference between staged and un-staged changes

# Show changes on before commit(staged)
git diff --staged
# Note: difference between staged changes and last commit

# Specify a file to show changes on before commit(un-staged)
git diff <file>

# Specify a file to show changes on before commit(staged)
git diff --staged <file>

# Show Diff on vscode
git difftool
git difftool --staged
# Note:is no difference than vscode will now show
# Note:difftool setting above "Git Configuration" section

# Using with cached
git diff --cached
git difftool --cached
# Note:(--staged and --cached are synonyms)


# Show differences between two branches

#Using with cached
git diff --cached
git difftool --cached
#Note:(--staged and --cached are synonyms)

git diff <branch> <branch>
```

## Remove, Move & Rename files

```bash
# Remove a file from the staging area and working dir
git rm <file>

# Remove a file from the staging area
git rm --cached <file>

# Remove a fils and whole directory from the staging area
git rm -r <directory>
# Note: -r is recursive

# Rename a file from the staging area and working dir
git mv <file> <file>.txt
```

## Revert & Reset files from the staging area

```bash
# Undo / revert un-staged changes on a file
git checkout <file>
git checkout

# Undo / revert last staged file
git reset HEAD <file>
# All files
git reset HEAD

# Unstaging a Staged File with git restore(staged)
git restore --staged <file>

# Unmodified a Modified File with git restore(un-staged)
git restore <file>
# NOTE: Use restore instead of checkout and reset

# Undo / revert last commit
git revert HEAD
# With message
git revert HEAD -m <message>

# Amend the most recent commit
git commit --amend
# With new message
git commit --amend -m <message>

# Revert an old commit
git revert commit-id

# Remove/Delete commit without message/ extra commit
# -n, --no-commit don't automatically commit
git revert -n head
git revert -n master~5..master~2
```

TODO: Different between `git reset` and `git revert` and `git restore`

## Stash staging

```bash
# Stash your changes so you can add them to a different branch.
git stash

# View all stashed list
git stash list

# Bring back stash back.
git stash pop

# Add the latest stash while keeping it in the list
git stash apply

# View a condensed version or files of the changes in the latest stash
git stash show
git stash show -p

# View specific stash `stash@{0}`.
git stash show <stash_name>
git stash show stash@{1}

# Drop Stash
git stash drop
git stash drop <stash_name>
```

## **`git branch`**

```bash
# Show all branches
git branch
git branch -a

# Show remote branches that Git is tracking
git branch -r

# Show each branch tracking a remote branch. or
# Show the current branch and its upstream branch.
git branch -vv

# Show branches that are not not merging with current branch
git branch --no-merged
git branch --merge

# Show the last commit on each branch
git branch -v

# Show the remote tracking branch for a specific branch
git branch -vv --list <branch_name>

# Show branches based on a pattern
git branch --list <pattern>
# ex: git branch --list 'feature/*'
# ex: git branch --list "*bug*"
# ex: git branch --list "*-fix"

# Show current branch name
git branch --show-current

# Create a new branch
git branch <branch>

# Create the branch's reflog
git branch --create-reflog <new-branch>

# Switch to a new branch
git checkout <branch>
git switch <branch>
# NOTE: Use switch instead of checkout

# Return to the previous branch
git switch -

# Create and switch to a new branch
git checkout -b <branch>
git switch -c <branch>

# Delete a branch
git branch -d <branch>
git branch --delete <branch>
# force delete
git branch -D <branch>

# Rename a branch and its reflog
git branch -m <branch> <branch>
# Ex: git branch -m <old branch> <new branch>
# Rename a branch even if target exists
git branch -M <branch>
```

### 🎎 Merge branch

```bash
# Merge a branch into the current branch
git merge <branch>

# Abort a conflicted merge
git merge --abort

# Merge a remote repo with local repo
git merge <remote|alias>/<branch>
# Ex: git merge origin/main
```

### 🤖 Remote Branch: Tracking, Deleting, Renaming

```bash
# Fetch the latest remote branches from the remote repository
git fetch <remote>

# Create the remote branch and pushing local branch to the remote
git push origin <local_branch_name>:<remote_branch_name>
# Ex: git push origin dev:dev

# Track a remote branch
git branch --track <branch> <remote>/<branch>
# Push to remote branch that is tracked by local branch
git push origin HEAD:<branch>
# Ex: git branch --track dev origin/dev
# Ex: git push origin HEAD:dev
# ExL git pull origin dev

# Track and Switch
git checkout -b <branch> <remote>/<branch>
# Ex:git checkout -b main origin/main

# Track an existing local branch to an existing remote branch
git branch --set-upstream-to=<remote>/<remote_branch> <local_branch>
git branch --set-upstream-to=origin/dracula dragon

git push origin --delete <branch>
# Ex: git push origin --delete <old branch>

# Rename a remote branch
git branch -m <old_branch> <new_branch>
git push <remote> --delete <old_branch>
git push <remote> <new_branch>

# Unset the upstream info
git branch --unset-upstream <branch>
```

## Remote Repositories

```bash
# Show remote repositories/url
git remote -v
git remote

# Add a remote repository
git remote add <alias> <url>
# Ex: git remote add origin https://github.com/<author>/a-journey-with-git-to-github.git

# Rename remote repository
git remote rename old-name new-name

# Remove a remote
git remote rm <remote|alias>

# More information about a remote repository
git remote show <remote|alias>
git ls-remote <remote|alias>

# Delete a remote branch
git push --delete <remote|alias> <branch>
```

## Push Repositories

```bash
# Push all changes in the current branch to a remote repository
git push
git push -u <remote|alias> <branch>

# Push a new branch to a remote repository
git push -u <remote|alias> <branch>
```

## Pull

```bash
# Pull all changes from a remote repository
git pull
```

## Fetch Repositories

```bash
# Fetch all changes from a remote repository
git fetch

# fetch from all remotes
git fetch --all
```

## Update Remote

```bash
# Update changes from a remote branch without automatically merging
git remote update
```

## Git Rebase

```bash
# Rebase a branch onto another branch
git rebase <branch>
git rebase main

# Continue rebasing
git rebase --continue

#Manipulate commits
git rebase --interactive HEAD~2
# note: HEAD~2 means you will have a chance to change the last two commits.
# note: it will open with nano.
# pick => use commit,
# d drop => remove commit,
# r reword => use commit but edit commit message,
# s squash => use commit but meld into previous commit

# Manipulate all commits
git rebase --interactive --root
# note: When you rebase interactively it changes all those `hashes`, so git sees them as different commits. If you were to try and `merge` this into `main`, it wouldn't work because they don't share the same history anymore. For this reason, you don't want to do an interactive rebase where you go back passed commits unique to the `branch` you are on.

# Squashing commits will take a bunch of commits and turn them into one.


```

## Git Tag

```bash
# Show all tags
git tag
git tag -l

# Add a new tag to the current commit(Annotated Tag)
git tag -a <tag> -m <message>

# Add a new tag to the current commit(Lightweight Tag)
git tag <tag>

# Add and tag to specific commits
git tag -a <tag> -m <message> <commit>

# Push tags to remote repository
git push <remote> <tag>

# push All tags to remote repository
git push <remote> --tags

# Push all tags to remote repository (Annotated Tag only)
git push <remote> --follow-tags

# Delete a Tag (local only)
git tag -d <tag>

# Delete a Tag (remote only)
git push <remote> --delete <tag>
git push <remote> :refs/tags/<tag>

# Checkout a Tag
git checkout <tag>

# Create a new branch from a tag
git switch -c <branch>

# Switch to a Tag
git checkout <tag>
```
