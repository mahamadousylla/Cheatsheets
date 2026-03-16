# Git Cheatsheet

## Setup
| Command | Action |
|---------|--------|
| `git init` | Initialize a new local repo |
| `git clone <url>` | Clone a remote repo locally |
| `git remote add origin <url>` | Link local repo to a remote |
| `git remote -v` | Show remote URLs. Shows you the URLs your local repo is connected to — useful to verify you're pushing/pulling from the right place |

---

## Staging & Committing
| Command | Action |
|---------|--------|
| `git add <file>` | Stage a file |
| `git add .` | Stage all changes |
| `git commit -m "message"` | Commit staged changes |
| `git commit --amend` | Edit the last commit message (before pushing) |

---

## Pushing & Pulling
| Command | Action |
|---------|--------|
| `git push` | Push to remote |
| `git push -u origin <branch>` | Push + set upstream (first push) |
| `git push --set-upstream origin <branch>` | Same as as shorthand version git push -u origin |
| `git pull` | Fetch + merge remote changes |
| `git fetch` | Download remote changes without merging |

---

## Branches
| Command | Action |
|---------|--------|
| `git branch` | List local branches |
| `git branch <name>` | Create a new branch |
| `git checkout <branch>` | Switch to branch |
| `git checkout -b <branch>` | Create + switch in one step |
| `git checkout -b <branch> <file>` | Restores a file from the remote
  branch |
| `git merge <branch>` | Merge branch into current |
| `git branch -d <branch>` | Delete a branch |
| `git push origin --delete <branch>` | Delete a branch |

---

## Undoing Things
| Command | Action |
|---------|--------|
| `git restore <file>` | Discard unstaged changes in a file |
| `git restore --staged <file>` | Unstage a file |
| `git reset --mixed HEAD~1` | Undo last commit, move all changes to unstaged |
| `git reset --soft HEAD~1` | Undo last commit, keep changes staged |
| `git reset --hard HEAD~1` | Undo last commit, discard changes |
| `git revert <commit>` | Create a new commit that undoes a commit (safe for shared branches) |

---

## Inspecting
| Command | Action |
|---------|--------|
| `git log` | Show commit history |
| `git log --oneline` | Compact commit history |
| `git diff HEAD` | Shows all, both staged and unstaged changes compared to the last commit |
| `git diff` | Show unstaged changes. Includes only the lines changed. |
| `git diff --staged` | Show staged changes |
| `git diff <option1> <option2>` | Compares two things and shows the line-by-line differences between them. Can be two branches (git diff main origin/main), two commits, a branch and a commit |
| `git show <commit>` | Show details of a commit. Defaults to last commit if none is specified. Shows just the line changes. Include metadata (author, date, message) |
| `git show --name-only` | Same as above but shows only the filename |
| `git status` | Show changed/staged/untracked files. Only the filenames and their state are shown |
| `git blame <file>` | Show who changed each line |

---

## Stash
| Command | Action |
|---------|--------|
| `git stash` | Temporarily save uncommitted changes |
| `git stash pop` | Restore stashed changes |
| `git stash apply` | Restore stashed changes. Use apply if you want to apply the same stash to multiple branches. |
| `git stash drop` | Removes the most recent stash |
| `git stash list` | List all stashes |
| `git stash show -p <stash>` | Shows the full line-by-line diff of a stash. Without -p you only get the filenames. i.e stash@{0} |
---

## Rebase (use with care)
It moves your branch's commits on top of another branch, as if you had branched off later.

main:    A - B - C
feature:     D - E

after git rebase main:
main:    A - B - C
feature:         D - E

Instead of a merge commit, your commits get reapplied on top of the latest code. Keeps history cleaner but rewrites commits, so avoid it on shared branches.

You branched off B, made commits D and E, but meanwhile C was added to main. Rebase brings in C, re-applies your commits on top of it, resolves any conflicts, then you merge back into main and push.

| Command | Action |
|---------|--------|
| `git rebase <branch>` | Reapply commits on top of another branch |
| `git rebase -i HEAD~n` | Interactive rebase — squash/edit last n commits. Common use case — squash several small commits into one clean commit before merging |
| `git rebasev--continue` | Tells git to move on and re-apply the next commit. You run it after each conflict until all commits are replayed. |


Example:

# you're on feature branch, which has commits D and E
# main has new commit C

  git checkout feature
  git rebase main

# git now re-applies D and E on top of C
# fix conflicts if any, then

  git rebase --continue
---

## Config
It's for setting your git preferences — things like your identity, default editor, default branch name, and behavior settings. Changes apply either globally (all repos) with --global or just for the current repo without it.

| Command | Action |
|---------|--------|
| `git config --global user.name "Name"` | Set your name (attached to every commit) |
| `git config --global user.email "email"` | Set your email (attached to every commit) |
| `git config --list` | Show all current config settings |
| `git config --global core.editor "code --wait"` | Set VS Code as default editor |
| `git config --global init.defaultBranch main` | Set default branch name to main |

---