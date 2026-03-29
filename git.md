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
| `git commit -am "message"` | Stages all modified tracked files and commits in one step — combines git add and git commit -m. Does not include new/untracked files. |
| `git commit --amend` | Edit the last commit message (before pushing) |

---

## Pushing & Pulling
| Command | Action |
|---------|--------|
| `git push` | Push to remote |
| `git push -u origin <branch>` | Push + set upstream (first push) |
| `git push --set-upstream origin <branch>` | Same as as shorthand version git push -u origin |
| `git fetch` | Download remote changes without merging. Good if you want to see what's changed before deciding to merge. Can be paired with git diff |
| `git pull` | Fetch + merge remote changes |

---

## Branches
| Command | Action |
|---------|--------|
| `git branch` | List local branches |
| `git branch <name>` | Create a new branch |
| `git checkout <branch>` | Switch to branch |
| `git checkout -b <branch>` | Create + switch in one step |
| `git checkout -b <branch> <file>` | Restores a file from the remote branch |
| `git switch <branch>` | Switch to a branch (newer alternative to git checkout <branch>) |
| `git switch -` | Switch back to the previous branch you were on |
| `git merge <branch>` | Merge branch into current |
| `git branch -d <branch>` | Delete a branch |
| `git push origin --delete <branch>` | Delete a branch |

---

## Undoing Things
| Command | Action |
|---------|--------|
| `git restore <file>` | Discard unstaged changes in a file, restores file to last commit |
| `git restore --staged <file>` | Unstage a file |
| `git reset --mixed HEAD~1` | Undo last commit, move all changes to unstaged |
| `git reset --soft HEAD~1` | Undo last commit, keep changes staged |
| `git reset --hard HEAD~1` | Undo last commit, discard changes |
| `git reset --mode <commit_hash>` | Moves the branch back to that commit_hash.

The mixed mode will unstage any changes made after that commit_hash. 

The soft mode will keep any changes in staged made after that commit_hash.

The hard mode will delete any changes after that commit_hash.

commit_hash can come from git log. |
| `git revert <commit>` | Creates a new commit that inverses the changes from the target commit — history is preserved, nothing is rewritten |

### Revert explained

Use `git revert` when a bad commit is already on a shared branch (like main) and others have pulled it. You can't `git reset` because that would rewrite shared history. Instead, revert adds a new commit on top that undoes it.

- The original commit **stays in history forever** — revert never removes anything
- If you try to merge that same code in again, Git will show no differences because the original commit hash is already in the history

To bring the reverted changes back:

1. **Revert the revert** — `git revert <revert-commit-hash>`
2. **Cherry-pick the original** — Run `git cherry-pick <original-commit-hash>` for each commit (copies the changes and creates a new commit with a new hash)
3. **Manually re-apply the changes** and commit fresh

---

## Inspecting
| Command | Action |
|---------|--------|
| `git log` | Show commit history of your current branch - commit hash, author, date, and message for each commit. Each commit is associated with a unique hash |
| `git log --oneline` | Compact commit history |
| `git rev-list --count HEAD` | Total number of commits on the current branch |
| `git rev-list --count origin/main..HEAD` | Number of commits on your branch that aren't on origin/main (i.e. not yet merged/pushed) |
| `git reflog` | Show a log of everywhere HEAD has pointed — every checkout, commit, reset, rebase. Useful for recovering lost commits |
| `git blame <file>` | Show who changed each line. It shows who last modified each line of a file — the commit hash, author, and date next to every line. Useful for tracking down when and why a specific line was changed. |

### Undoing with reflog

The flow is:

1. `git reflog` — find the hash of where you were before the unwanted action
2. `git reset --hard <hash>` — restore to that point

The reflog lists every HEAD movement in order, so:

- If you just made one bad action, the second entry (index `HEAD@{1}`) is where you were before it
- If you made multiple actions you want to undo, you'd go further down the list

The second hash is just "one step back." You pick whichever entry represents the state you want to return to.

- 1 bad action → HEAD@{1} (2nd entry)
- 2 bad actions → HEAD@{2} (3rd entry)
- and so on


## Diffing
| Command | Action |
|---------|--------|
| `git diff` | Show unstaged changes. Includes only the lines changed. File(s) under VSCode>Changes vs File(s) from the last commit. If you have staged changes for that file, they will not show in the diff. |
| `git diff --staged` | Show staged changes compared to the last commit. File(s) under VSCode>Staged Changes vs File(s) from the last commit. |
| `git diff HEAD` | Shows all, both staged and unstaged changes compared to the file(s) in the last commit |
| `git diff <option1> <option2>` | Compares two things and shows the line-by-line differences between them. Can be two branches (git diff main origin/main), two commits, a branch and a commit |
| `git show <commit>` | Show details of a commit. Defaults to last commit if none is specified. Shows just the line changes. Include metadata (author, date, message) |
| `git show --name-only` | Same as above but shows only the filename |
| `git status` | Show changed/staged/untracked files. Only the filenames and their state are shown |

---

## Stash
| Command | Action |
|---------|--------|
| `git stash` | Temporarily save uncommitted changes |
| `git stash pop` | Restore stashed changes and removes that stash |
| `git stash apply` | Restore stashed changes. Use apply if you want to apply the same stash to multiple branches. |
| `git stash drop` | Removes the most recent stash |
| `git stash list` | List all stashes |
| `git stash show -p <stash>` | Shows the full line-by-line diff of a stash. Without -p you only get the filenames. i.e stash@{0} |
---

## Chery pick

| `git cherry-pick` | It lets you pick a specific commit from another branch and apply it to your current branch. |

## Rebase (use with care)

| Command | Action |
|---------|--------|
| `git rebase <branch>` | Reapply commits on top of another branch. If you have uncommitted changes, git will just refuse to start and tell you to commit or stash them first. (look into autoStash) |
| `git rebase -i HEAD~n` | Interactive rebase — squash/edit last n commits. Common use case — squash several small commits into one clean commit before merging |
| `git rebase -i --root` | Interactive rebase. It opens the interactive rebase editor showing all commits in the repo from the very first one, instead of just the last N commits.  |
| `git rebase --continue` | Tells git to move on 
and re-apply the next commit. You run it after each conflict until all commits are replayed. |
| `git rebase --edit-todo` | Reopens the rebase instruction list mid-rebase so you can fix it and
continue. Git pauses, you edit, then `git rebase --continue` picks up where it left off. |
| `git rebase --abort` | Cancels the entire rebase and restores your branch to exactly how it was before you started. |





### Rebase and Dangers explained

It moves your branch's commits on top of another branch, as if you had branched off later.

Instead of a merge commit, your commits get replayed/reapplied on top of the latest code. Keeps history cleaner but rewrites commits, so avoid it on shared feature branches.

You branched off B, made commits D and E, but meanwhile C was added to main. Rebase brings in C, re-applies your commits, D and E, on top of it, resolves any conflicts, then you merge back into main and push.

main:    A → B → C
feature:     ↓
             D → E        (branched off B)

git checkout feature
git rebase main

After:

main:    A → B → C        (untouched)
feature:         ↓
                 D' → E'  (new hashes, only you have these)
    

Danger — teammate also has feature

you:  D' → E'   (after rebase + force push)
them: D  → E    (stale — Git sees a diverged history)

you:  D' → E'   (after rebase + force push)
them: D  → E    (stale — Git sees a diverged history)

Rule: if anyone else has a copy of your branch, don't rebase it.

**The rule in one sentence:** whichever branch is being rebased gets new commit hashes — so if anyone else has that branch, their copy instantly diverges from yours.

Top half shows the safe case: you rebase feature, main stays untouched, D and E become D' and E' but nobody else has them so it doesn't matter.

Bottom half shows the danger: once you force-push D' and E', your teammate is stuck with stale D and E that Git now treats as a completely different history.

The typical flow is:

1. Rebase feature onto main locally
2. Force push to update your remote feature branch
3. Open the MR from your feature branch

Notes:

git rebase main (means "rebase the current branch onto main." Main is just the reference point you're rebasing onto — it doesn't move.)

Main's commits are never rewritten — they're just the fixed base you're replaying your feature commits on top of.

### Rebase Interactive

Squash is the most common use for git rebase -i, but -i gives you a few more options:

Options:

  - pick — keep commit as is
  - squash / s — merge into previous commit, keep
  both messages. Allows you to edit the commit message. Opens an editor for you to change the message, then continues
  - fixup / f — merge into previous commit, discard
  this commit's message
  - reword / r — keep commit but edit the message. pauses the rebase on that commit and opens an
  editor for you to change the message, then
  continues
  - edit / e — pause to amend the commit. pauses the rebase on that commit and takes you back to your normal command prompt, letting you make changes to the actual files (not just the message). When done you run git rebase --continue to move on
  - drop / d — delete the commit
  

### Rebase Continue

It's what you run after resolving a merge conflict mid-rebase.

When Git replays your commits on top of the new base, it does them one at a time. If a commit conflicts, Git pauses and asks you to fix it. Once you've resolved the conflict and staged the fix with git add, you run git rebase --continue to tell Git to carry on replaying the remaining commits.

The other options at that point are git rebase --skip (skip that commit entirely) or git rebase --abort (bail out and go back to how things were before the rebase started).


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