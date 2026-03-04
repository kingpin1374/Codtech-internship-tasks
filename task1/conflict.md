# Git Conflict Resolution Task

This document provides a step-by-step guide on how a merge conflict was created, identified, and resolved within the `Codtech-internship-tasks` repository.

---

## 1. Initial File Creation (Master Branch)
The process began by creating a base file on the main branch to establish a starting point for the conflict.

* **File**: `task1/README.md`
* **Content**: "Hey this is a file to create merge conflict"
* **Action**: Staged and committed the file to the `master` branch
* **Command**: `git commit -m "create a file for git merge conflict"`

## 2. Creating a Divergent Branch
To simulate a conflict, a second branch was created to modify the same file independently.

* **Branch Switch**: Switched to a new branch named `branch1`
* **Modification**: Edited `README.md` with different text: "this is to create conflict on merging both branches"
* **Command**: `git commit -m "create a file for git merge conflict"`

## 3. Triggering the Merge Conflict
The conflict was triggered when attempting to combine the two different versions of the same file.

* **Switch Back**: Returned to the `master` branch
* **Merge Command**: `git merge branch1`
* **Error Encountered**: `CONFLICT (add/add): Merge conflict in task1/README.md`
* **Status**: Automatic merge failed; Git required manual intervention to resolve the differences

## 4. Manual Resolution Process
The conflict markers were manually removed to finalize the file content.

* **Identification**: Opened `README.md` to see the conflict markers (`<<<<<<< HEAD`, `=======`, `>>>>>>> branch1`)
* **Edit**: Used `nano` to remove the markers and keep the desired text
* **Staging**: Ran `git add .` to mark the conflict as resolved
* **Final Commit**: Ran `git commit -m "conflict fixed"` to complete the merge

## 5. Final Verification and Push
After the resolution, the repository state was verified and synced with the remote server.

* **Verification**: Ran `git merge branch1` again, resulting in "Already up to date"
* **Push to GitHub**: Successfully pushed the resolved master branch to `github.com:kingpin1374/Codtech-internship-tasks.git`
