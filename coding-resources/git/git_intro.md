---
layout: page
title: Git Introduction
parent: Git
grand_parent: Coding Resources
nav_order: 1
---

# Git cheat sheet

This is a minimal, practical Git cheat sheet for everyday use.

---

## Install + open Terminal

### Check if Git is installed
```bash
git --version
```

If you are using macOS, you may be prompted to install developer tools. Accept it.

If you are using Windows, you may be prompted to install Git. Accept it.

Open Terminal and go to your project:
```bash
cd path/to/your/project
```
If you do not know what 'cd' does, please refer to the command line resources.

---

## One-time setup (do this once)

Set your name + email:
```bash
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
```

Check config:
```bash
git config --list
```

---

## Basic

### See what changed
```bash
git status
```

### Stage changes
Stage one file:
```bash
git add file.txt
```
You are telling git to track the changes in the file. In layman's terms, you are telling git to watch the file and tell you if it changes.

Stage everything:
```bash
git add .
```
The dot means "all files".

### Commit
```bash
git commit -m "Explain what you changed"
```

You are telling git to save the changes you made to the file. The -m flag means "message" and you should write a short message about what you changed. A good commit message is like a short description of what you did.


### Start a new repo
```bash
git init
```


### Clone an existing repo
```bash
git clone <repo-url>
```
For example, if the repo url is https://github.com/uiuc-ae353/ae353-sp26.git, you can clone it by running:
```bash
git clone https://github.com/uiuc-ae353/ae353-sp26.git
```

## Advanced
---

### See history

```bash
git log --oneline
```

### Branches (basic)

See branches:
```bash
git branch
```
A branch is like a separate timeline for your project. You can work on different features in different branches. For example, you can create a branch to work on a new feature and then eventually merge it into the main branch when you are done. This is useful because it allows you to work on different features in parallel.

Create + switch:
```bash
git switch -c feature/my-change
```

Switch back:
```bash
git switch main
```

### Pull, push, remotes

Show remotes:
```bash
git remote -v
```
A remote is like a remote server that stores your repository. You can pull the latest changes from the remote server to your local repository and push your changes to the remote server.

Pull latest:
```bash
git pull
```
Pulling is like downloading the latest changes from the remote server to your local repository. For example everytime we upload a new project, you will be asked to 'pull' the latest changes to your local repository i.e., this is equivalent to downloading the latest version of the project to your local machine.


Push your commits:
```bash
git push
```

First push of a new branch:
```bash
git push -u origin feature/my-change
```

Pushing is like uploading your changes to the remote server. For example everytime you want to upload your changes to the remote server, you will be asked to 'push' your changes to the remote server i.e., this is equivalent to uploading your changes to the remote server. 

You cannot push your changes to the remote server:
- if you have not pulled the latest changes from the remote server to your local repository.
- if you have not committed your changes to the local repository.
- if you do not have permission to push to the remote server, for this particular course, you will not be able to push to the class' remote server, but instead if you make a new repo on your own github account, you can push to your own remote server.

### Ignore files with .gitignore

Create `.gitignore` in the repo root.

Example:
```gitignore
node_modules/
dist/
.env
.DS_Store
```

---

### Undo the common stuff

Unstage (keep edits):
```bash
git restore --staged file.txt
```

Discard local changes (DANGEROUS):
```bash
git restore file.txt
```

Change last commit message (if not pushed):
```bash
git commit --amend -m "New message"
```

---

### Stash (pause work)

```bash
git stash
git stash pop
```

---

## Quick safety rules

- Do not commit secrets (keys, passwords, `.env`).
- When unsure, run `git status`.
- Commit often in small chunks.


