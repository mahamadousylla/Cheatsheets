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
| `git status` | Show changed/staged/untracked files. Only the filenames and their state are shown |
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
| `git merge <branch>` | Merge branch into current |
| `git branch -d <branch>` | Delete a branch |

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
| `git blame <file>` | Show who changed each line |

---

## Stash
| Command | Action |
|---------|--------|
| `git stash` | Temporarily save uncommitted changes |
| `git stash pop` | Restore stashed changes |
| `git stash apply` | Restore stashed changes. Use apply if you want to apply the same stash to multiple branches. |
| `git stash list` | List all stashes |

---

## Rebase (use with care)
| Command | Action |
|---------|--------|
| `git rebase <branch>` | Reapply commits on top of another branch |
| `git rebase -i HEAD~n` | Interactive rebase — squash/edit last n commits |
