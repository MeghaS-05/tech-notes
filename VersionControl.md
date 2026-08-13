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
