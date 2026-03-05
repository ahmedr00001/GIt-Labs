# Git History Manipulation Lab

This repository contains practical exercises for managing Git history, completed as part of the ITI System Administration track. The lab demonstrates how to create, delete, amend, and revert commits, as well as how to handle forced updates to a remote repository.

## Lab Objectives
1. Make 4 initial commits.
2. Delete the last two commits from the history.
3. Add a new commit after the deletion.
4. Amend a commit to include new file modifications and change the commit message.
5. Understand the `git revert` command and revert a specific commit.

---

## Execution Steps

### 1. Creating the Initial 4 Commits
Files were created and committed sequentially to build a commit history:
```bash
# Commit 1
git add .
git commit -m "add id file"
git push -u origin main

# Commit 2
git add .
git commit -m "Adding python file"
git push

# Commit 3
git add .
git commit -m "test file"
git push

# Commit 4
git add .
git commit -m "mod test.py file"
git push
```

### 2. Deleting the Last Two Commits
To remove the last two commits (`mod test.py file` and `test file`) and move the `HEAD` pointer back, a hard reset was used:
```bash
git reset --hard HEAD^^
```

### 3. Adding a New Commit After Deletion
A new file (`after delete.txt`) was created and committed to the newly reset branch. Because the local history diverged from the remote repository, a force push was required.
```bash
git add .
git commit -m "commit after delete"
git push --force
```

### 4. Amending the Last Commit
Modifications were made (adding "lab Done" to a file), and the previous commit was amended to include these changes along with a new commit message: `"finish"`.
```bash
# Amend the previous commit and change the message
git commit --amend -m "finish"

# Force push to update the remote branch with the amended commit
git push --force
```

### 5. Reverting a Commit
To safely undo the changes from a specific previous commit (the commit that added the python file), `git revert` was used:
```bash
git revert f806
git push
```

---

## What is `git revert`?

`git revert` is a safe, non-destructive way to undo changes in Git. 

Unlike `git reset` (which deletes commit history), `git revert` takes the changes made in a specific commit, does the exact opposite of them, and creates a **brand new commit** with those reversed changes. 

This is the standard and safest way to undo changes on a shared public branch because it preserves the repository's history and prevents conflicts for other collaborators.