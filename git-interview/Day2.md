# **Git Practice Workflow: Basics to Advanced**

Git is an essential tool for version control in software development. This guide provides a step-by-step workflow for practicing **basic** and **advanced Git commands**, with clear explanations and examples.

---

## **1. Git Basics**

### **1.1. Initialize a Git Repository**
- **Command:**
  ```bash
  git init
  ```
- **Explanation:**
  - Initializes a new Git repository in the current directory.
- **Practice:**
  1. Create a new folder:
     ```bash
     mkdir git-practice && cd git-practice
     ```
  2. Initialize the Git repository:
     ```bash
     git init
     ```

---

### **1.2. Check the Status of a Repository**
- **Command:**
  ```bash
  git status
  ```
- **Explanation:**
  - Displays the state of the working directory and staging area.
- **Practice:**
  1. Create a new file:
     ```bash
     echo "Hello, World!" > file.txt
     ```
  2. Check the status:
     ```bash
     git status
     ```

---

### **1.3. Add Files to the Staging Area**
- **Command:**
  ```bash
  git add <filename>
  ```
- **Explanation:**
  - Moves changes from the working directory to the staging area.
- **Practice:**
  ```bash
  git add file.txt
  ```

---

### **1.4. Commit Changes**
- **Command:**
  ```bash
  git commit -m "Your commit message"
  ```
- **Explanation:**
  - Records changes in the repository with a message.
- **Practice:**
  ```bash
  git commit -m "Initial commit"
  ```

---

### **1.5. View Commit History**
- **Command:**
  ```bash
  git log
  ```
- **Explanation:**
  - Displays the commit history.
- **Practice:**
  ```bash
  git log
  ```

---

### **1.6. Create and Switch Branches**
- **Command:**
  ```bash
  git branch <branch_name>
  git switch <branch_name>
  ```
- **Explanation:**
  - Creates and switches to a new branch.
- **Practice:**
  ```bash
  git branch feature-branch
  git switch feature-branch
  ```

---

### **1.7. Merge Branches**
- **Command:**
  ```bash
  git merge <branch_name>
  ```
- **Explanation:**
  - Combines changes from one branch into another.
- **Practice:**
  1. Switch to the main branch:
     ```bash
     git switch main
     ```
  2. Merge the feature branch:
     ```bash
     git merge feature-branch
     ```

---

### **1.8. Clone a Repository**
- **Command:**
  ```bash
  git clone <repository_url>
  ```
- **Explanation:**
  - Creates a local copy of a remote repository.
- **Practice:**
  ```bash
  git clone https://github.com/user/repository.git
  ```

---

## **2. Git Advanced Commands**

### **2.1. Stashing Changes**
- **Command:**
  ```bash
  git stash
  git stash list
  git stash pop
  ```
- **Explanation:**
  - Temporarily saves changes without committing them.
- **Practice:**
  1. Modify `file.txt`:
     ```bash
     echo "Temporary change" >> file.txt
     ```
  2. Stash the changes:
     ```bash
     git stash
     ```
  3. View the stash:
     ```bash
     git stash list
     ```
  4. Apply the stash:
     ```bash
     git stash pop
     ```

---

### **2.2. Resolving Merge Conflicts**
- **Scenario:**
  - Two branches modify the same line in a file.
- **Practice:**
  1. Create a conflict:
     - On `main` branch:
       ```bash
       echo "Main branch change" > conflict.txt
       git add conflict.txt
       git commit -m "Change in main branch"
       ```
     - On `feature` branch:
       ```bash
       git switch -c feature-branch
       echo "Feature branch change" > conflict.txt
       git add conflict.txt
       git commit -m "Change in feature branch"
       ```
  2. Merge `feature-branch` into `main`:
     ```bash
     git switch main
     git merge feature-branch
     ```
  3. Resolve conflict manually in `conflict.txt` and commit:
     ```bash
     git add conflict.txt
     git commit -m "Resolved merge conflict"
     ```

---

### **2.3. Undoing Commits**
- **Command:**
  ```bash
  git reset --soft <commit_hash>
  git reset --hard <commit_hash>
  ```
- **Explanation:**
  - **Soft Reset:** Moves the HEAD to a previous commit but keeps changes in the staging area.
  - **Hard Reset:** Discards all changes after the specified commit.
- **Practice:**
  1. View commit history:
     ```bash
     git log
     ```
  2. Reset to a previous commit:
     ```bash
     git reset --soft <commit_hash>
     ```

---

### **2.4. Cherry-Picking Commits**
- **Command:**
  ```bash
  git cherry-pick <commit_hash>
  ```
- **Explanation:**
  - Applies a specific commit from one branch to another.
- **Practice:**
  1. Switch to `main`:
     ```bash
     git switch main
     ```
  2. Cherry-pick a commit from `feature-branch`:
     ```bash
     git cherry-pick <commit_hash>
     ```

---

### **2.5. Rewriting Commit History**
- **Command:**
  ```bash
  git rebase -i <base_commit>
  ```
- **Explanation:**
  - Interactively edit, reorder, or squash commits during rebase.
- **Practice:**
  ```bash
  git rebase -i HEAD~3
  ```

---

### **2.6. Viewing and Restoring Deleted Branches**
- **Command:**
  ```bash
  git reflog
  git checkout -b <branch_name> <commit_hash>
  ```
- **Explanation:**
  - `git reflog`: Lists all changes to the HEAD.
  - `git checkout`: Restores a branch from a specific commit.
- **Practice:**
  1. Delete a branch:
     ```bash
     git branch -d feature-branch
     ```
  2. Recover it using `reflog`:
     ```bash
     git reflog
     git checkout -b feature-branch <commit_hash>
     ```

---

## **3. Practice Tips**
1. Use GitHub repositories to practice interacting with remote repositories.
2. Simulate real-world scenarios like merge conflicts, undoing commits, and rebasing.
3. Document your learnings in a Markdown file to build a portfolio.

---

## **4. Key Takeaways**
- **Basics:** Learn how to initialize a repository, commit changes, and manage branches.
- **Advanced:** Practice stashing, rebasing, cherry-picking, and resolving conflicts.
- **Real-World Scenarios:** Simulate workflows to prepare for interviews and real projects.

---

*Prepared  by **Kotireddy*** 🚀  
**#Git #DevOps #VersionControl #InterviewPreparation**