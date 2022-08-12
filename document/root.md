# A Journey With Git To GitHub

[👨‍🎓 sizar corpse](https://github.com/sizarcorpse) | [👨‍🚀 ramiz imran sizar](https://github.com/ramizimran)

This document covers every basic command you need to do the vast majority of the things you’ll eventually spend your time doing with Git. By the end of the document, you should be able to configure and initialize a repository, begin and stop tracking files, and stage and commit changes.This document also show you how to set up Git to ignore certain files and file patterns, how to undo mistakes quickly and easily, how to browse the history of your project and view changes between commits, and how to push and pull from remote repositories.

## 🌍 Git Configuration

```bash
# View all of settings
git config -list --show-origin

# Check git configuration
git config --list
git config -l

# Set git configuration
# Set global configuration

#set name
git config --global users.name "<name>"

# get name
git config users.name

#set email
git config --global users.email "<email>"

#get email
git config users.email

#check credentials
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
#Note: after setup difftool, use "git difftool" instead of "git diff"
```

```bash
# Set Default Branch Name for
git config --global init.defaultBranch main
```

## 🚩 Initializing a Repository

```bash
#Initializing an existing directory as a Git repository
git init

#Clone/Retrieve an entire existing repository from via URL
git clone <url>

#With desire name
git clone <url> <name>
# Note:That command does the same thing as the previous one, but the target directory is called <name>.

```

## 🚚 Creating Snapshots and Staging

```bash

#Show the status of the current repository including staged, unstated, and untracked files
git status

#Show the status of the current repository including staged, unstated, and untracked files
git status -s
# ?? = untracked files, M = modified files, A = added files, D = deleted files, R = renamed files, C = copied files, U = updated files, ! = ignored files

#Add all files and folders recursively to the staging area
git add .

#Add single file to the staging area
git add <file>

#Add multiple files to the staging area
git add <file> <file>

#Add all files with a specific extension to the staging area
git add *.txt
```

## Git Ignore

```bash
# Create a .gitignore file
.gitignore

#Examine the contents of the .gitignore file
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

## 📦 Committing Staged

```bash

#Commit all staged files with long commit message
git commit

#Commit all staged files with a specific message
git commit -m "Initial commit"

#Commit all staged files without staging
git commit -a -m "Initial commit"
git commit -am "Initial commit"

#Show a specific commit
git show commit-id
```

## 🔭 Browsing Commit History

```bash
#Show commit history of the current repository
git log

#Show commit history including all files and their changes
git log -p

#Show commit history by one line
git log --oneline

#Reverse order
git log --reverse

#With reflog
git --reflog

#Show commit history with a specific number of commits
git log -n 5
git log 5
#Note: Shows the last 5 commits

#Show some statistics about the changes in each commit.
git log --stat

#Show commit log as a graph
git log --graph
#One line
git log --graph --oneline
#All
git log --all --graph --oneline
```

## 🥼 Diff whats changes on before commit (staged or un-staged)

```bash
#Show changes on before commit(un-staged)
git diff
#Note: difference between staged and un-staged changes

#Show changes on before commit(staged)
git diff --staged
#Note: difference between staged changes and last commit

#Specify a file to show changes on before commit(un-staged)
git diff <file>

#Specify a file to show changes on before commit(staged)
git diff --staged <file>

#SHow Diff on vscode
git difftool
git difftool --staged
#Note:is no difference than vscode will now show
#Note:difftool setting above "Git Configuration" section

#Using with cached
git diff --cached
git difftool --cached
#Note:(--staged and --cached are synonyms)

#Show differences between two branches
git diff <branch> <branch>
```

## 🗑 Remove files

```bash
#Remove a file from the staging area and working dir
git rm <file>

#Remove a file from the staging area
git rm --cached <file>

#Remove a fils and whole directory from the staging area
git rm -r <directory>
#Note: -r is recursive

#Rename a file from the staging area and working dir
git mv <file> <file>.txt
```

## 📝Revert & Reset files from the staging area

```bash
#Undo / revert un-staged changes on a file
git checkout <file>
git checkout

#Undo / revert last staged file
git reset HEAD <file>
#All files
git reset HEAD

#Amend the most recent commit
git commit --amend
#With new message
git commit --amend -m "New message"

#Undo / revert last commit
git revert HEAD
#with message
git revert HEAD -m "New message"

#Revert an old commit
git revert commit-id
```

## 🧰 Branching

```bash
#Show all branches
git branch

# Remote branches that Git is tracking
git branch -r

#Create a new branch
git branch <branch>

#Switch to a new branch
git checkout <branch>

#Create and switch to a new branch
git checkout -b <branch>

#Delete a branch
git branch -d <branch>
git branch --delete <branch>
```

## 🎎 Merging branch

```bash
#Merge a branch into the current branch
git merge <branch>

#Abort a conflicted merge
git merge --abort

#Merge a remote repo with local repo
git merge <remote|alias>/<branch>
#Ex: git merge origin/main
```

## ⛅ Remote Repositories

```bash
# Show remote repositories/url
git remote -v
git remote

# Add a remote repository
git remote add <alias> <url>
# Ex: git remote add origin https://github.com/<author>/a-journey-with-git-to-github.git

# Rename remote repository
git remote rename old-name new-name

# Remove a remote repository
git remote rm <remote|alias>

# More information about a remote repository
git remote show <remote|alias>

# Delete a remote branch
git push --delete <remote|alias> <branch>
```

## 🚀 Push Repositories

```bash
# Push all changes in the current branch to a remote repository
git push
git push -u <remote|alias> <branch>

# Push a new branch to a remote repository
git push -u <remote|alias> <branch>
```

## 🧯 Pull

```bash
# Pull all changes from a remote repository
git pull
```

## 🚓 Fetch Repositories

```bash
# Fetch all changes from a remote repository
git fetch
```

## 🧨 Update Remote

```bash
# Update changes from a remote branch without automatically merging
git remote update
```

## 🏤 Git Rebase

```bash
# Rebase a branch onto another branch
git rebase <branch>
```
