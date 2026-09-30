## 1. Introduction

**Git** — A distributed version control system that tracks changes in source code over time.

**GitHub** — A cloud-based hosting platform for Git repositories, used for collaboration, code review, and CI/CD.

---

## 2. Installation & Initial Setup

### 2.1 Install Git

Installs Git on your system.
**Syntax** — `sudo apt install git` (Linux) / `brew install git` (Mac) / download from git-scm.com (Windows)
**Example** — `sudo apt install git -y`

### 2.2 Check Git Version

Displays the installed Git version.
**Syntax** — `git --version` 

**Example** — `git --version` → `git version 2.44.0`

### 2.3 Set Username

Sets the global username used in commits.
**Syntax** — `git config --global user.name "Your Name"` **Example** — `git config --global user.name "Rohit Sharma"`

### 2.4 Set Email

Sets the global email used in commits.
**Syntax** — `git config --global user.email "you@example.com"` 

**Example** — `git config --global user.email "rohit@gmail.com"`

### 2.5 View All Configs

Lists all Git configuration settings.
**Syntax** — `git config --list`

**Example** — `git config --list`

### 2.6 Set Default Editor

Sets the default text editor for Git messages.
**Syntax** — `git config --global core.editor "code --wait"` 

**Example** — `git config --global core.editor "nano"`

---

## 3. Creating a Repository

### 3.1 Initialize a New Repo

Creates a new, empty Git repository in the current folder.
**Syntax** — `git init`  **Example** — `git init my-project`

### 3.2 Clone an Existing Repo

Downloads a copy of an existing remote repository.
**Syntax** — `git clone <repo-url>`  **Example** — `git clone https://github.com/user/repo.git`

### 3.3 Clone a Specific Branch

Clones only a particular branch instead of the default one.
**Syntax** — `git clone -b <branch-name> <repo-url>` **Example** — `git clone -b dev https://github.com/user/repo.git`

---

## 4. Basic Workflow (Staging & Committing)

### 4.1 Check Status

Shows the current state of the working directory and staging area.
**Syntax** — `git status` **Example** — `git status`

### 4.2 Add a File to Staging

Moves a file from working directory to staging area.
**Syntax** — `git add <filename>` **Example** — `git add index.html`

### 4.3 Add All Files

Stages all modified/new files at once.
**Syntax** — `git add .`**Example** — `git add .`

### 4.4 Commit Changes

Saves staged changes to the local repository history.
**Syntax** — `git commit -m "message"` **Example** — `git commit -m "Added login page"`

### 4.5 Add + Commit Together

Stages and commits already-tracked files in one step.
**Syntax** — `git commit -am "message"` **Example** — `git commit -am "Fixed navbar bug"`

### 4.6 View Commit History

Shows the list of past commits.
**Syntax** — `git log` **Example** — `git log --oneline`

### 4.7 View Detailed History with Graph

Shows commit history as a visual branch graph.
**Syntax** — `git log --oneline --graph --all` **Example** — `git log --oneline --graph --all --decorate`

here —all is where Git shows commits reachable from **all local refs/branches**, so you can see other branches too and —decorate is to show labels.

---

## 5. Branching

### 5.1 List Branches

Shows all local branches.
**Syntax** — `git branch` **Example** — `git branch`

### 5.2 Create a New Branch

Creates a new branch without switching to it.
**Syntax** — `git branch <branch-name>` **Example** — `git branch feature-login`

### 5.3 Switch Branch

Switches your working directory to another branch.
**Syntax** — `git checkout <branch-name>` or `git switch <branch-name>` **Example** — `git switch feature-login`

### 5.4 Create & Switch in One Step

Creates a new branch and moves to it immediately.
**Syntax** — `git checkout -b <branch-name>` **Example** — `git checkout -b feature-signup`

### 5.5 Rename a Branch

Renames the current branch.
**Syntax** — `git branch -m <new-name>` **Example** — `git branch -m main`

### 5.6 Delete a Branch (local)

 Removes a local branch that's already merged.
**Syntax** — `git branch -d <branch-name>` **Example** — `git branch -d feature-login`

### 5.7 Force Delete a Branch

Removes a local branch even if it's not merged.
**Syntax** — `git branch -D <branch-name>` **Example** — `git branch -D old-feature`

---

## 6. Merging & Rebasing

### 6.1 Merge a Branch

Combines changes from another branch into the current branch.
**Syntax** — `git merge <branch-name>` **Example** — `git merge feature-login`

### 6.2 Rebase a Branch

Reapplies commits from current branch on top of another branch (linear history).
**Syntax** — `git rebase <branch-name>`**Example** — `git rebase main`

### 6.3 Abort a Rebase

Cancels an in-progress rebase and restores previous state.
**Syntax** — `git rebase --abort` **Example** — `git rebase --abort`

### 6.4 Continue a Rebase (after conflict fix)

Resumes rebase after resolving a conflict.
**Syntax** — `git rebase --continue` **Example** — `git rebase --skip`

### 6.5 Skip a Rebase

Skip this commit → move on
**Syntax** — `git rebase --skip` **Example** — `git rebase --continue`

---

## 7. Working with Remotes

### 7.1 Add a Remote

Links a local repo to a remote (e.g., GitHub) repository.
**Syntax** — `git remote add origin <repo-url>` **Example** — `git remote add origin https://github.com/user/repo.git`

### 7.2 View Remotes

Lists all remote connections for the repo.
**Syntax** — `git remote -v` **Example** — `git remote -v`

### 7.3 Remove a Remote

Detaches a remote connection from the local repo.
**Syntax** — `git remote remove <remote-name>` **Example** — `git remote remove origin`

### 7.4 Rename a Remote

Changes the name of an existing remote.
**Syntax** — `git remote rename <old-name> <new-name>` **Example** — `git remote rename origin upstream`

### 7.5 Change Remote URL

Updates the URL of an existing remote.
**Syntax** — `git remote set-url origin <new-url>` **Example** — `git remote set-url origin https://github.com/user/new-repo.git`

---

## 8. Push, Pull & Fetch

### 8.1 Push Changes

Uploads local commits to the remote repository.
**Syntax** — `git push origin <branch-name>` **Example** — `git push origin main`

### 8.2 Push and Set Upstream

Pushes a branch and links it to a remote branch for future pushes/pulls.
**Syntax** — `git push -u origin <branch-name>` **Example** — `git push -u origin feature-login`

### 8.3 Force Push

Overwrites remote history with local history (use carefully).
**Syntax** — `git push --force` **Example** — `git push --force origin main`

### 8.4 Fetch Changes

Downloads remote changes WITHOUT merging them into your branch.
**Syntax** — `git fetch origin` **Example** — `git fetch origin`

### 8.5 Fetch All Remotes

Fetches updates from every configured remote.
**Syntax** — `git fetch --all` **Example** — `git fetch --all`

### 8.6 Pull Changes

Fetches AND merges remote changes into the current branch.
**Syntax** — `git pull origin <branch-name>` **Example** — `git pull origin main`

### 8.7 Pull with Rebase

Pulls remote changes and rebases local commits on top (avoids merge commits).
**Syntax** — `git pull --rebase origin <branch-name>` **Example** — `git pull --rebase origin main`

---

## 9. Viewing Differences

### 9.1 View Unstaged Changes

Shows differences between working directory and staging area.
**Syntax** — `git diff` **Example** — `git diff`

### 9.2 View Staged Changes

Shows differences between staging area and last commit.
**Syntax** — `git diff --staged` **Example** — `git diff --staged`

### 9.3 Compare Two Branches

Shows differences between two branches.
**Syntax** — `git diff <branch1> <branch2>` **Example** — `git diff main dev`

---

## 10. Undoing Changes

### 10.1 Unstage a File

Removes a file from the staging area (keeps changes).
**Syntax** — `git restore --staged <file>`**Example** — `git restore --staged index.html`

### 10.2 Discard Changes in a File

**Definition** — Reverts a file back to its last committed state.
**Syntax** — `git restore <file>`**Example** — `git restore index.html`

### 10.3 Undo Last Commit (keep changes)

**Definition** — Removes the last commit but keeps changes staged.
**Syntax** — `git reset --soft HEAD~1`**Example** — `git reset --soft HEAD~1`

### 10.4 Undo Last Commit (unstage changes)

**Definition** — Removes the last commit and unstages changes, but keeps files.
**Syntax** — `git reset --mixed HEAD~1`**Example** — `git reset HEAD~1`

### 10.5 Undo Last Commit (delete changes)

**Definition** — Completely removes the last commit and all its changes.
**Syntax** — `git reset --hard HEAD~1`**Example** — `git reset --hard HEAD~1`

### 10.6 Revert a Commit

**Definition** — Creates a new commit that undoes a previous commit (safe for shared history).
**Syntax** — `git revert <commit-hash>`**Example** — `git revert a1b2c3d`

---

## 11. Stashing

### 11.1 Stash Changes

**Definition** — Temporarily saves uncommitted changes so you can switch branches cleanly.
**Syntax** — `git stash`**Example** — `git stash save "wip login form"`

### 11.2 List Stashes

**Definition** — Shows all saved stashes.
**Syntax** — `git stash list`**Example** — `git stash list`

### 11.3 Apply a Stash

**Definition** — Restores stashed changes without removing them from the stash list.
**Syntax** — `git stash apply`**Example** — `git stash apply stash@{0}`

### 11.4 Pop a Stash

**Definition** — Restores the latest stashed changes and removes it from the list.
**Syntax** — `git stash pop`**Example** — `git stash pop`

### 11.5 Drop a Stash

**Definition** — Deletes a specific stash entry.
**Syntax** — `git stash drop`**Example** — `git stash drop stash@{0}`

### 11.6 Clear All Stashes

**Definition** — Deletes all stashed entries.
**Syntax** — `git stash clear`**Example** — `git stash clear`

---

## 12. Tags

### 12.1 Create a Tag

**Definition** — Marks a specific commit (usually a release point) with a label.
**Syntax** — `git tag <tag-name>`**Example** — `git tag v1.0.0`

### 12.2 Create an Annotated Tag

**Definition** — Creates a tag with metadata (author, date, message).
**Syntax** — `git tag -a <tag-name> -m "message"`**Example** — `git tag -a v1.0.0 -m "First release"`

### 12.3 Push Tags to Remote

**Definition** — Uploads local tags to GitHub.
**Syntax** — `git push origin <tag-name>`**Example** — `git push origin v1.0.0`

### 12.4 Push All Tags

**Definition** — Uploads every local tag to remote.
**Syntax** — `git push origin --tags`**Example** — `git push origin --tags`

### 12.5 Delete a Tag (local)

**Definition** — Removes a tag from your local repo.
**Syntax** — `git tag -d <tag-name>`**Example** — `git tag -d v1.0.0`

### 12.6 Delete a Tag (remote)

**Definition** — Removes a tag from the remote repo.
**Syntax** — `git push origin --delete <tag-name>`**Example** — `git push origin --delete v1.0.0`

---

## 13. .gitignore

### 13.1 Ignore Files

**Definition** — A file listing patterns of files/folders Git should not track.
**Syntax** — create `.gitignore` and add patterns
**Example** —

```
node_modules/
.env
*.log
```

### 13.2 Stop Tracking an Already-Tracked File

**Definition** — Removes a file from Git tracking without deleting it from disk.
**Syntax** — `git rm --cached <file>`**Example** — `git rm --cached .env`

---

## 14. Advanced Commands

### 14.1 Cherry-pick a Commit

**Definition** — Applies a specific commit from another branch onto the current branch.
**Syntax** — `git cherry-pick <commit-hash>`**Example** — `git cherry-pick a1b2c3d`

### 14.2 View Reflog

**Definition** — Shows a log of all HEAD movements — useful for recovering "lost" commits.
**Syntax** — `git reflog`**Example** — `git reflog`

### 14.3 Recover Lost Commit

**Definition** — Restores a commit found via reflog.
**Syntax** — `git checkout <commit-hash>`**Example** — `git checkout a1b2c3d`

### 14.4 Bisect (Find Buggy Commit)

**Definition** — Binary-searches commit history to find which commit introduced a bug.
**Syntax** — `git bisect start`**Example** — `git bisect start` → `git bisect bad` → `git bisect good v1.0`

### 14.5 Blame a File

**Definition** — Shows who changed each line of a file and in which commit.
**Syntax** — `git blame <file>`**Example** — `git blame app.js`

### 14.6 Add a Submodule

**Definition** — Embeds another Git repository inside your current repository.
**Syntax** — `git submodule add <repo-url>`**Example** — `git submodule add https://github.com/user/lib.git libs/lib`

### 14.7 Update Submodules

**Definition** — Pulls the latest changes for all submodules.
**Syntax** — `git submodule update --remote`**Example** — `git submodule update --remote`

### 14.8 Squash Commits (Interactive Rebase)

**Definition** — Combines multiple commits into one for a cleaner history.
**Syntax** — `git rebase -i HEAD~<n>`**Example** — `git rebase -i HEAD~3`

### 14.9 Set Up a Git Hook

**Definition** — A script that auto-runs at specific Git events (e.g., before commit).
**Syntax** — edit file in `.git/hooks/`**Example** — edit `.git/hooks/pre-commit` and make it executable: `chmod +x .git/hooks/pre-commit`

### 14.10 Show a Specific Commit

**Definition** — Displays the full details/diff of one commit.
**Syntax** — `git show <commit-hash>`**Example** — `git show a1b2c3d`

### 14.11 Clean Untracked Files

**Definition** — Deletes untracked files from the working directory.
**Syntax** — `git clean -f`**Example** — `git clean -fd` (removes untracked files and folders)

---

## 15. Removing Git From a Project (Locally)

### 15.1 Remove Git Tracking (keep files)

**Definition** — Deletes Git's internal tracking data but keeps all your project files intact — the folder is no longer a Git repo.
**Syntax** — `rm -rf .git` (Mac/Linux) or `rmdir /s /q .git` (Windows CMD)
**Example** — `rm -rf .git`

> ⚠️ This does NOT touch GitHub — it only removes Git tracking from your local folder.
> 

---

## 16. Deleting a GitHub Repository (Remote)

### 16.1 Delete via GitHub Website

**Definition** — Permanently deletes a repository from GitHub's servers.
**Steps** —

1. Go to your repo → **Settings**
2. Scroll to the bottom **"Danger Zone"**
3. Click **Delete this repository**
4. Type `username/repo-name` to confirm
5. Click **I understand the consequences, delete this repository**

### 16.2 Delete via GitHub CLI

**Definition** — Deletes a GitHub repo using the terminal (requires `gh` CLI installed & authenticated).
**Syntax** — `gh repo delete <owner>/<repo> --yes`**Example** — `gh repo delete rohit/my-project --yes`

> ⚠️ This is irreversible. There is no "undo" for a deleted GitHub repository.
> 

---

## 17. GitHub-Specific Concepts

### 17.1 Fork a Repo

**Definition** — Creates your own copy of someone else's repository under your GitHub account.
**Action** — Click **Fork** button on the repo page.
**Example** — Fork `https://github.com/facebook/react` to `https://github.com/you/react`

### 17.2 Pull Request (PR)

**Definition** — A request to merge your branch's changes into another repo/branch, usually for review.
**Action** — On GitHub → **Pull Requests → New Pull RequestExample** — Open PR from `feature-login` → `main`

### 17.3 Add Upstream (for forks)

**Definition** — Links your fork to the original repository so you can sync updates.
**Syntax** — `git remote add upstream <original-repo-url>`**Example** — `git remote add upstream https://github.com/facebook/react.git`

### 17.4 Sync Fork with Upstream

**Definition** — Pulls the latest changes from the original repo into your fork.
**Syntax** — `git fetch upstream && git merge upstream/main`**Example** — `git fetch upstream` then `git merge upstream/main`

### 17.5 Clone via SSH

**Definition** — Clones using SSH keys instead of HTTPS (no password prompts).
**Syntax** — `git clone git@github.com:user/repo.git`**Example** — `git clone git@github.com:rohit/my-project.git`

### 17.6 Generate SSH Key

**Definition** — Creates a key pair to authenticate with GitHub without a password.
**Syntax** — `ssh-keygen -t ed25519 -C "your_email@example.com"`**Example** — `ssh-keygen -t ed25519 -C "rohit@gmail.com"`

### 17.7 GitHub Actions (CI/CD basics)

**Definition** — Automates workflows (tests, builds, deployments) triggered by repo events.
**Syntax** — create `.github/workflows/main.yml`**Example** —

yaml

```yaml
name: CI
on: [push]
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - run: echo "Running tests..."
```

---

## 18. Quick Cheat Sheet

| Command | Purpose |
| --- | --- |
| `git init` | Start a new repo |
| `git clone <url>` | Copy a remote repo |
| `git status` | Check current state |
| `git add .` | Stage all changes |
| `git commit -m "msg"` | Save changes |
| `git push` | Upload to remote |
| `git pull` | Download + merge from remote |
| `git fetch` | Download without merging |
| `git branch` | List branches |
| `git checkout -b <name>` | Create + switch branch |
| `git merge <branch>` | Merge branch into current |
| `git log --oneline` | View history |
| `git stash` | Save WIP changes temporarily |
| `git reset --hard HEAD~1` | Undo last commit fully |
| `git revert <hash>` | Safely undo a commit |
| `rm -rf .git` | Remove Git from local project |
| `gh repo delete <repo>` | Delete GitHub repo |

---

## 19. Extra / Lesser-Known Commands

### 19.1 Amend Last Commit

**Definition** — Edits the most recent commit (message and/or staged changes) instead of creating a new one.
**Syntax** — `git commit --amend -m "new message"`**Example** — `git commit --amend -m "Fixed typo in README"`

### 19.2 Rename/Move a File (Git-tracked)

**Definition** — Renames or moves a file and stages the change in one step.
**Syntax** — `git mv <old-name> <new-name>`**Example** — `git mv old.js new.js`

### 19.3 Remove a File (Git-tracked)

**Definition** — Deletes a file from disk and stages the deletion.
**Syntax** — `git rm <file>`**Example** — `git rm unused.css`

### 19.4 Shallow Clone

**Definition** — Clones a repo with limited commit history for faster downloads.
**Syntax** — `git clone --depth <n> <url>`**Example** — `git clone --depth 1 https://github.com/user/repo.git`

### 19.5 Filter Log by Author

**Definition** — Shows only commits made by a specific author.
**Syntax** — `git log --author="<name>"`**Example** — `git log --author="Rohit"`

### 19.6 Filter Log by Date

**Definition** — Shows commits made within a date range.
**Syntax** — `git log --since="<date>" --until="<date>"`**Example** — `git log --since="2026-01-01" --until="2026-02-01"`

### 19.7 Search Commit Messages

**Definition** — Finds commits whose message matches a pattern.
**Syntax** — `git log --grep="<text>"`**Example** — `git log --grep="fix bug"`

### 19.8 Show Commit Stats

**Definition** — Shows how many lines were added/removed per file in each commit.
**Syntax** — `git log --stat`**Example** — `git log --stat -3`

### 19.9 Abort a Merge

**Definition** — Cancels an in-progress merge (e.g., during conflicts) and restores pre-merge state.
**Syntax** — `git merge --abort`**Example** — `git merge --abort`

### 19.10 Merge Without Fast-Forward

**Definition** — Forces a merge commit even when a fast-forward is possible (keeps branch history visible).
**Syntax** — `git merge --no-ff <branch>`**Example** — `git merge --no-ff feature-login`

### 19.11 Abort Cherry-pick

**Definition** — Cancels an in-progress cherry-pick operation.
**Syntax** — `git cherry-pick --abort`**Example** — `git cherry-pick --abort`

### 19.12 List All Tags

**Definition** — Displays every tag in the repository.
**Syntax** — `git tag -l`**Example** — `git tag -l "v1.*"`

### 19.13 Describe Current Commit

**Definition** — Shows the nearest tag relative to the current commit (useful for versioning builds).
**Syntax** — `git describe --tags`**Example** — `git describe --tags` → `v1.0.0-3-gA1b2c3d`

### 19.14 List Tracked Files

**Definition** — Lists all files currently tracked by Git.
**Syntax** — `git ls-files`**Example** — `git ls-files`

### 19.15 List Remote Branches Without Cloning

**Definition** — Shows branches/refs on a remote repo without downloading it.
**Syntax** — `git ls-remote <url>`**Example** — `git ls-remote https://github.com/user/repo.git`

### 19.16 Check Repo Integrity

**Definition** — Verifies the integrity of Git objects in the repository, finds dangling commits.
**Syntax** — `git fsck`**Example** — `git fsck --full`

### 19.17 Cleanup & Optimize Repo

**Definition** — Compresses repo data and removes unreachable objects to save space.
**Syntax** — `git gc`**Example** — `git gc --aggressive`

### 19.18 Create a Git Alias

**Definition** — Creates a shortcut for a longer Git command.
**Syntax** — `git config --global alias.<shortname> "<command>"`**Example** — `git config --global alias.co checkout` → now use `git co main`

### 19.19 Export Repo as Archive

**Definition** — Bundles the repo (or part of it) into a zip/tar file without the `.git` history.
**Syntax** — `git archive --format=zip -o <file>.zip HEAD`**Example** — `git archive --format=zip -o project.zip HEAD`

### 19.20 Create Patch Files

**Definition** — Generates `.patch` files from commits, useful for sharing changes without a remote.
**Syntax** — `git format-patch -<n>`**Example** — `git format-patch -1 HEAD`

### 19.21 Apply a Patch

**Definition** — Applies a `.patch` file's changes to the current repo.
**Syntax** — `git apply <file>.patch`**Example** — `git apply fix.patch`

### 19.22 Rebase Onto a Different Base

**Definition** — Moves a range of commits onto a new base branch/commit (advanced history rewriting).
**Syntax** — `git rebase --onto <newbase> <oldbase> <branch>`**Example** — `git rebase --onto main old-base feature-x`

### 19.23 Sparse Checkout (partial repo)

**Definition** — Checks out only specific folders of a large repo instead of the whole thing.
**Syntax** — `git sparse-checkout set <folder>`**Example** — `git sparse-checkout set docs/`

### 19.24 Multiple Working Trees

**Definition** — Lets you check out multiple branches into separate folders from the same repo simultaneously.
**Syntax** — `git worktree add <path> <branch>`**Example** — `git worktree add ../hotfix hotfix-branch`

### 19.25 Sign a Commit (GPG)

**Definition** — Cryptographically signs a commit to verify authorship (shows "Verified" badge on GitHub).
**Syntax** — `git commit -S -m "message"`**Example** — `git commit -S -m "Signed release commit"`

### 19.26 Attach Notes to a Commit

**Definition** — Adds extra metadata/notes to a commit without changing its hash.
**Syntax** — `git notes add -m "<note>"`**Example** — `git notes add -m "Reviewed by QA" HEAD`

### 19.27 Track Upstream Branch Status

**Definition** — Shows local branches along with their ahead/behind status vs. remote.
**Syntax** — `git branch -vv`**Example** — `git branch -vv`

---

## 20. GitHub CLI (`gh`) — Extra Commands

### 20.1 Authenticate CLI

**Definition** — Logs the `gh` CLI into your GitHub account.
**Syntax** — `gh auth login`**Example** — `gh auth login`

### 20.2 Create a Repo from CLI

**Definition** — Creates a new GitHub repository without opening a browser.
**Syntax** — `gh repo create <name>`**Example** — `gh repo create github-notes --public`

### 20.3 Clone via CLI

**Definition** — Clones a repo using the `gh` tool (handles auth automatically).
**Syntax** — `gh repo clone <owner>/<repo>`**Example** — `gh repo clone rohit/my-project`

### 20.4 Create a Pull Request from CLI

**Definition** — Opens a PR directly from the terminal.
**Syntax** — `gh pr create`**Example** — `gh pr create --title "Add login" --body "Implements login form" --base main`

### 20.5 View PR Status

**Definition** — Shows the status of pull requests in the current repo.
**Syntax** — `gh pr status`**Example** — `gh pr status`

### 20.6 Create an Issue from CLI

**Definition** — Opens a new GitHub issue from the terminal.
**Syntax** — `gh issue create`**Example** — `gh issue create --title "Bug: login fails" --body "Steps to reproduce..."`

### 20.7 Create a Release

**Definition** — Publishes a tagged release with notes/binaries on GitHub.
**Syntax** — `gh release create <tag>`**Example** — `gh release create v1.0.0 --notes "First stable release"`

---

## 21. Plumbing (Low-Level / Internal) Commands

> These are rarely used directly — Git uses them internally. Good to know for deep debugging or building tools on top of Git.
> 

### 21.1 Hash an Object

**Definition** — Computes the SHA hash of a file's content (as Git would store it) without saving it.
**Syntax** — `git hash-object <file>`**Example** — `git hash-object index.html`

### 21.2 View Object Content

**Definition** — Displays the raw content/type/size of any Git object (blob, tree, commit).
**Syntax** — `git cat-file -p <hash>`**Example** — `git cat-file -p a1b2c3d`

### 21.3 Update the Index Manually

**Definition** — Directly adds/modifies entries in the staging area (used internally by `git add`).
**Syntax** — `git update-index --add <file>`**Example** — `git update-index --add newfile.txt`

### 21.4 Write a Tree Object

**Definition** — Creates a tree object from the current staging area (snapshot of files/folders).
**Syntax** — `git write-tree`**Example** — `git write-tree`

### 21.5 Create a Commit Object Manually

**Definition** — Creates a commit object from a tree, without touching branches (low-level version of `git commit`).
**Syntax** — `git commit-tree <tree-hash> -m "message"`**Example** — `git commit-tree 4b825dc -m "manual commit"`

### 21.6 Parse a Revision

**Definition** — Converts a branch name, tag, or shorthand reference into its full commit hash.
**Syntax** — `git rev-parse <ref>`**Example** — `git rev-parse HEAD`

### 21.7 List Commit Hashes in Order

**Definition** — Lists commit hashes matching given criteria (used internally by `git log`).
**Syntax** — `git rev-list <ref>`**Example** — `git rev-list --count HEAD`

### 21.8 Read/Update a Symbolic Reference

**Definition** — Views or updates a symbolic ref like `HEAD` (which points to the current branch).
**Syntax** — `git symbolic-ref HEAD`**Example** — `git symbolic-ref HEAD refs/heads/main`

### 21.9 Update a Reference Directly

**Definition** — Manually points a ref (like a branch) to a specific commit.
**Syntax** — `git update-ref refs/heads/<branch> <commit-hash>`**Example** — `git update-ref refs/heads/main a1b2c3d`

### 21.10 Pack Objects

**Definition** — Compresses loose Git objects into a single packfile to save space.
**Syntax** — `git pack-objects <base-name>`**Example** — `git rev-list --objects --all | git pack-objects pack`

### 21.11 Unpack Objects

**Definition** — Extracts objects from a packfile back into individual loose objects.
**Syntax** — `git unpack-objects < <packfile>`**Example** — `git unpack-objects < pack-abc.pack`

### 21.12 Compare Two Commit Ranges

**Definition** — Compares two different series of commits (e.g., before/after a rebase) to see what actually changed.
**Syntax** — `git range-diff <range1> <range2>`**Example** — `git range-diff main~5..main main~5..feature`

### 21.13 Summarize Commits by Author

**Definition** — Shows a count of commits grouped by each author.
**Syntax** — `git shortlog -sn`**Example** — `git shortlog -sn --all`

### 21.14 Verify a Signed Commit

**Definition** — Checks the GPG signature of a signed commit to confirm authenticity.
**Syntax** — `git verify-commit <commit-hash>`**Example** — `git verify-commit a1b2c3d`

### 21.15 Verify a Signed Tag

**Definition** — Checks the GPG signature of a signed tag.
**Syntax** — `git verify-tag <tag-name>`**Example** — `git verify-tag v1.0.0`

### 21.16 Run Repo Maintenance

**Definition** — Runs background optimization tasks (gc, prefetch, commit-graph updates) on a schedule or on demand.
**Syntax** — `git maintenance run`**Example** — `git maintenance start` (schedules automatic maintenance)

---

## 22. Config, Line-Endings & File Behavior

### 22.1 Unset a Config Value

**Definition** — Removes a previously set Git configuration value.
**Syntax** — `git config --unset <key>`**Example** — `git config --global --unset user.email`

### 22.2 Handle Line Endings (Windows/Mac/Linux)

**Definition** — Controls automatic conversion of line endings (CRLF/LF) between OS types.
**Syntax** — `git config --global core.autocrlf <true|input|false>`**Example** — `git config --global core.autocrlf input`

### 22.3 Cache Credentials Temporarily

**Definition** — Stores your Git login credentials in memory for a set time so you're not prompted repeatedly.
**Syntax** — `git config --global credential.helper cache`**Example** — `git config --global credential.helper 'cache --timeout=3600'`

### 22.4 Store Credentials Permanently

**Definition** — Saves credentials to disk (less secure, but no repeated prompts).
**Syntax** — `git config --global credential.helper store`**Example** — `git config --global credential.helper store`

### 22.5 .gitattributes File

**Definition** — A file that defines per-file-type rules for line endings, diff behavior, and merge strategy.
**Syntax** — create `.gitattributes` in repo root
**Example** —

```
*.sh text eol=lf
*.png binary
*.jpg binary
```

### 22.6 Git LFS (Large File Storage)

**Definition** — An extension that replaces large files (videos, datasets) with lightweight pointers, storing the actual files separately.
**Syntax** — `git lfs install` then `git lfs track "<pattern>"`**Example** — `git lfs track "*.psd"`

---

## 23. Alternatives to Submodules & History Rewriting

### 23.1 Git Subtree

**Definition** — Merges another repository into a subdirectory of your repo (alternative to submodules, no extra clone step needed for users).
**Syntax** — `git subtree add --prefix=<folder> <repo-url> <branch>`**Example** — `git subtree add --prefix=libs/ui https://github.com/user/ui-lib.git main --squash`

### 23.2 Rewrite History to Remove a File (filter-repo)

**Definition** — Permanently removes a file (e.g., a leaked secret) from the entire Git history. Requires the `git-filter-repo` tool.
**Syntax** — `git filter-repo --path <file> --invert-paths`**Example** — `git filter-repo --path secrets.env --invert-paths`

> ⚠️ Rewrites all commit hashes — coordinate with your team and force-push afterward.
> 

---

## 24. GitHub Platform Features (Beyond Git Commands)

These aren't Git commands but are essential GitHub-side features referenced alongside them.

### 24.1 Branch Protection Rules

**Definition** — Repo settings that prevent direct pushes to a branch (e.g., `main`) and require PR reviews/checks before merging.
**Location** — Repo → Settings → Branches → Add rule

### 24.2 CODEOWNERS File

**Definition** — A file that auto-assigns reviewers to a PR based on which files were changed.
**Location** — `.github/CODEOWNERS`**Example** —

```
*.js   @frontend-team
/docs/ @docs-team
```

### 24.3 GitHub Secrets

**Definition** — Encrypted environment variables used securely inside GitHub Actions workflows.
**Location** — Repo → Settings → Secrets and variables → Actions

### 24.4 GitHub Environments

**Definition** — Named deployment targets (e.g., staging, production) with their own secrets and protection rules.
**Location** — Repo → Settings → Environments

### 24.5 GitHub Pages

**Definition** — Hosts a static website directly from a GitHub repository branch/folder for free.
**Location** — Repo → Settings → Pages

### 24.6 Gists

**Definition** — Small, shareable snippets of code hosted on GitHub, separate from full repositories.
**Action** — Go to gist.github.com → create new gist

### 24.7 Dependabot

**Definition** — An automated bot that scans dependencies for vulnerabilities and opens PRs to update them.
**Location** — Repo → Settings → Security → Dependabot

### 24.8 GitHub Projects (Boards)

**Definition** — Kanban-style boards built into GitHub for tracking issues/PRs as tasks.
**Location** — Repo → Projects tab → New project
