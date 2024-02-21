---
description: Basic Git Commands
---

# 📔 Cheatsheet

### Git Commands and Their Uses

#### Basic Commands

* `git init`: Initializes a new Git repository.
* `git clone [url]`: Clones an existing repository from the given URL.
* `git add [file]`: Adds a file to the staging area.
* `git commit -m "[message]"`: Commits the staged changes with a commit message.
* `git status`: Shows the status of changes as untracked, modified, or staged.
* `git log`: Displays the commit history.

#### Branching & Merging

* `git branch`: Lists all local branches.
* `git branch [branch-name]`: Creates a new branch.
* `git checkout [branch-name]`: Switches to the specified branch.
* `git merge [branch]`: Merges the specified branch into the current branch.
* `git branch -d [branch-name]`: Deletes the specified branch.

#### Remote Repositories

* `git remote add [name] [url]`: Adds a new remote repository.
* `git fetch [name]`: Fetches the branches and their respective commits from the remote repository.
* `git pull [remote] [branch]`: Fetches and merges changes from the remote branch to your local branch.
* `git push [remote] [branch]`: Pushes your local branch commits to the remote repository branch.

#### Undo Changes

* `git checkout -- [file]`: Discards changes in the working directory.
* `git reset [file]`: Removes the file from the staging area but preserves its contents.
* `git revert [commit]`: Creates a new commit that undoes the changes made in the specified commit.
* `git reset --hard [commit]`: Resets the index and working directory to the state of the specified commit.
