# **Git Advanced Notes with Command-Line Examples**

This guide is designed to help learners understand and practice advanced Git commands using Git Bash. Follow along with the examples to enhance your Git skills!

---

## **1. Stashing Changes**
- **Command:**
  ```bash
  git stash
  git stash list
  git stash pop
  ```
- **Purpose:**
  Temporarily saves uncommitted changes for later use.

- **Example Workflow:**
  1. Modify a file:
     ```bash
     echo "Temporary change" >> file.txt
     ```
  2. Stash the changes:
     ```bash
     git stash
     ```
  3. Check the stash list:
     ```bash
     git stash list
     ```
  4. Apply the stashed changes:
     ```bash
     git stash pop
     ```

---

## **2. Resolving Merge Conflicts**
- **Scenario:**
  Two branches modify the same line in a file, causing a conflict.

- **Commands:**
  ```bash
  git merge <branch_name>
  git status
  # Resolve conflicts manually
  git add <file_name>
  git commit
  ```

- **Example Workflow:**
  1. On `main` branch:
     ```bash
     echo "Main branch change" > conflict.txt
     git add conflict.txt
     git commit -m "Change in main branch"
     ```
  2. On a new branch:
     ```bash
     git checkout -b feature-branch
     echo "Feature branch change" > conflict.txt
     git add conflict.txt
     git commit -m "Change in feature branch"
     ```
  3. Merge the feature branch into `main`:
     ```bash
     git checkout main
     git merge feature-branch
     ```
  4. Resolve the conflict in `conflict.txt`, then:
     ```bash
     git add conflict.txt
     git commit -m "Resolved merge conflict"
     ```

---

## **3. Cherry-Picking Commits**
- **Command:**
  ```bash
  git cherry-pick <commit_hash>
  ```
- **Purpose:**
  Apply a specific commit from one branch to another.

- **Example Workflow:**
  1. Find the commit hash:
     ```bash
     git log feature-branch
     ```
  2. Cherry-pick the commit:
     ```bash
     git cherry-pick <commit_hash>
     ```

---

## **4. Interactive Rebase**
- **Command:**
  ```bash
  git rebase -i HEAD~<n>
  ```
- **Purpose:**
  Edit, squash, or reorder commits.

- **Example Workflow:**
  1. Start an interactive rebase for the last 3 commits:
     ```bash
     git rebase -i HEAD~3
     ```
  2. Use the interactive menu to:
     - Mark commits as `pick`, `squash`, or `edit`.
  3. Save and exit to apply the changes.

---

## **5. Resetting Commits**
- **Commands:**
  ```bash
  git reset --soft <commit_hash>
  git reset --hard <commit_hash>
  ```
- **Purpose:**
  - **Soft Reset:** Moves HEAD to a previous commit but keeps changes in the staging area.
  - **Hard Reset:** Discards all changes after the specified commit.

- **Example Workflow:**
  1. View commit history:
     ```bash
     git log
     ```
  2. Reset to a previous commit:
     ```bash
     git reset --soft <commit_hash>
     ```

---

## **6. Restoring Deleted Branches**
- **Command:**
  ```bash
  git reflog
  git checkout -b <branch_name> <commit_hash>
  ```
- **Purpose:**
  Recover a branch that has been deleted.

- **Example Workflow:**
  1. Delete a branch:
     ```bash
     git branch -d feature-branch
     ```
  2. Find the commit hash in the reflog:
     ```bash
     git reflog
     ```
  3. Restore the branch:
     ```bash
     git checkout -b feature-branch <commit_hash>
     ```

---

## **7. Debugging with `git bisect`**
- **Commands:**
  ```bash
  git bisect start
  git bisect good <commit_hash>
  git bisect bad <commit_hash>
  ```
- **Purpose:**
  Find the commit that introduced a bug.

- **Example Workflow:**
  1. Start the bisect:
     ```bash
     git bisect start
     git bisect good <commit_hash>
     git bisect bad <commit_hash>
     ```
  2. Test each commit and mark it:
     ```bash
     git bisect good
     git bisect bad
     ```
  3. End the bisect:
     ```bash
     git bisect reset
     ```

---

## **Key Takeaways**
1. Use `git stash` to temporarily save changes.
2. Learn to resolve merge conflicts manually.
3. Apply specific changes using `git cherry-pick`.
4. Clean up your commit history with interactive rebase.
5. Recover deleted branches with `git reflog`.
6. Debug issues efficiently using `git bisect`.

---

*Prepared for students by **Kotireddy***  
**#Git #DevOps #GitBash #VersionControl**

---
**Thank You for Visiting**  
I hope this repository helps you in your Git learning journey.  
Feel free to share this GitHub link to help others! 🚀