Complete DevOps Interview Questions and Answers
This document covers topics from basic to advanced levels. Kindly ensure you practice each tool to remember the concepts easily and explain them confidently to the panelists.

Note: If you have any questions, feel free to reach out at devopskotireddy@gmail.com.

For AWS Cloud tutorials, please visit: https://www.youtube.com/@cloudops-k

========Linux=======


How do you find all files larger then 100MB in a Directory   and its sub- directories …


## ✅ 1. Scenario: Server Disk Full Suddenly

**Question:**  
A production server suddenly stops responding. You try to SSH but it’s very slow. After logging in, you notice the disk is 100% full. How would you resolve this?

**Answer:**
```bash
df -h
du -sh /* 2>/dev/null | sort -hr | head -10
> /var/log/messages
yum clean all
```

**Explanation:**  
This scenario is common in production. I follow a structured approach—check space, trace file growth, clean or archive. It shows my awareness of file systems, log management, and system recovery.

---

## ✅ 2. Scenario: CPU Usage is High

**Question:**  
A developer reports the application is very slow. You suspect high CPU usage. How do you investigate?

**Answer:**
```bash
top
ps -eo pid,ppid,cmd,%mem,%cpu --sort=-%cpu | head
systemctl restart <servicename>
```

**Explanation:**  
I check system metrics using `top`, `ps`, and act based on the issue (e.g., looping process). This reflects hands-on troubleshooting and good decision-making in performance issues.

---

## ✅ 3. Scenario: Service Fails to Start

**Question:**  
A web service (e.g., Apache) fails to start on boot. How will you troubleshoot?

**Answer:**
```bash
systemctl status httpd
journalctl -xe
apachectl configtest
netstat -tuln | grep :80
```

**Explanation:**  
I approach this step-by-step: verify the service state, examine logs, validate config, and check port conflicts. It proves structured problem-solving with knowledge of systemd and networking.

---

## ✅ 4. Scenario: User Cannot Login via SSH

**Question:**  
A team member cannot SSH into a server. What steps would you take to resolve the issue?

**Answer:**
```bash
systemctl status sshd
id username
passwd -S username
ls -ld ~/.ssh
ls -l ~/.ssh/authorized_keys
tail -f /var/log/secure
```

**Explanation:**  
This checks for SSH service issues, user account problems, file permissions, and logs. It shows in-depth SSH knowledge and ability to handle real-time access issues securely.

---

## ✅ 5. Scenario: Crontab Not Working

**Question:**  
A scheduled backup script in crontab isn’t running. How do you debug it?

**Answer:**
```bash
crontab -l
systemctl status crond
grep CRON /var/log/cron
# Example cron job with logging
0 1 * * * /path/to/script.sh >> /tmp/backup.log 2>&1
```

**Explanation:**  
I verify cron syntax, service status, and logs. Adding logs to the script helps in debugging silently failing jobs. This shows my command over automation and job scheduling.

=====================================

## ✅ 6. Scenario: Permission Denied When Running a Script

**Question:**  
A user runs a shell script but gets a "Permission denied" error. How would you resolve it?

**Answer:**
```bash
ls -l script.sh
chmod +x script.sh
```

**Explanation:**  
The issue is usually missing execute permission. I use `ls -l` to verify and `chmod +x` to fix. This shows basic but critical knowledge of Linux permissions and script execution.

---

## ✅ 7. Scenario: Port 80 is Already in Use

**Question:**  
You try to start Apache, but it fails because port 80 is already in use. How do you handle this?

**Answer:**
```bash
netstat -tuln | grep :80
lsof -i :80
kill -9 <PID>  # if safe to stop
```

**Explanation:**  
This shows the ability to identify conflicting services using `netstat` and `lsof`, and the judgment to safely terminate processes. It’s a real-world issue in multi-service environments.

---

## ✅ 8. Scenario: Root Password Forgotten

**Question:**  
You have physical access to a Linux machine but forgot the root password. How would you reset it?

**Answer:**
1. Reboot the machine.
2. In GRUB menu, edit the boot entry and add:
   ```
   init=/bin/bash
   ```
3. Once in shell:
   ```bash
   mount -o remount,rw /
   passwd root
   exec /sbin/init
   ```

**Explanation:**  
This is a critical recovery scenario. Shows knowledge of boot process, GRUB, single-user mode, and password recovery—great for proving deep system understanding.

---

## ✅ 9. Scenario: Swap Memory is Full

**Question:**  
The system is using too much swap memory and becoming slow. What would you do?

**Answer:**
```bash
free -h
swapon --show
top  # check swap-using processes
swapoff -a
swapon -a
```

**Explanation:**  
Demonstrates understanding of virtual memory, how to monitor it, and how to clear swap. You might also investigate the need for more RAM or optimize heavy applications.

---

## ✅ 10. Scenario: File Deleted Accidentally – Need Recovery

**Question:**  
A critical file was deleted accidentally from the system. Can it be recovered?

**Answer:**  
- If it's still open by a process:
  ```bash
  lsof | grep deleted
  cp /proc/<pid>/fd/<fd> /recovered_file
  ```
- Otherwise, restore from backup or snapshots (if available).

**Explanation:**  
This scenario shows creative use of `/proc` and `lsof` for emergency recovery. It also highlights the importance of having backup policies in place.

---
```

================================================================

## ✅ 1. Scenario: Find All Failed SSH Login Attempts

**Command Used:** `grep`

**Question:**  
You are asked to find all failed SSH login attempts from the logs. How would you do that?

**Answer:**
```bash
grep "Failed password" /var/log/secure
```

**Explanation:**  
This command filters lines from `/var/log/secure` that show failed login attempts. It's useful for security auditing and shows understanding of system logs and `grep` filtering.

---

## ✅ 2. Scenario: Get Only IP Addresses from Failed Logins

**Command Used:** `awk`

**Question:**  
From the failed SSH login entries, how do you extract just the IP addresses?

**Answer:**
```bash
grep "Failed password" /var/log/secure | awk '{print $11}'
```

**Explanation:**  
Here, `awk` is used to print the 11th field (which contains the IP). This scenario shows the power of `awk` in parsing structured text like log files.

---

## ✅ 3. Scenario: Replace a Configuration Parameter in a File

**Command Used:** `sed`

**Question:**  
You need to change `PermitRootLogin no` to `PermitRootLogin yes` in the ssh config. How would you do it?

**Answer:**
```bash
sed -i 's/^PermitRootLogin no/PermitRootLogin yes/' /etc/ssh/sshd_config
```

**Explanation:**  
This demonstrates real-world use of `sed` for in-place editing. It also reflects on secure configuration management, often part of sysadmin and DevOps tasks.

---

## ✅ 4. Scenario: Summarize Disk Usage from `df -h` Output

**Command Used:** `awk`

**Question:**  
You want to list all mount points along with their usage percentage. How would you do that?

**Answer:**
```bash
df -h | awk 'NR>1 {print $6, $5}'
```

**Explanation:**  
`awk` is used here to skip the header (`NR>1`) and print mount point (6th field) and usage (5th). This shows how `awk` can be used to filter and format output quickly.

---

## ✅ 5. Scenario: Count Occurrences of a Word in a File

**Command Used:** `grep`, `wc`

**Question:**  
You want to know how many times the word "error" appears in a log file. How?

**Answer:**
```bash
grep -i "error" /var/log/messages | wc -l
```

**Explanation:**  
Combining `grep` and `wc` counts the number of matching lines. Shows effective use of piping and log analysis — something interviewers love to hear.


-==================================================
## ✅ 1. Scenario: Check if Server Was Recently Rebooted

**Command Used:** `uptime`

**Question:**  
How can you check how long a server has been running, or if it was recently rebooted?

**Answer:**
```bash
uptime
```

**Explanation:**  
The `uptime` command shows how long the system has been running, number of users, and load averages. Useful in troubleshooting to confirm if a server was rebooted unexpectedly or recently patched.

---

## ✅ 2. Scenario: Investigate High Load Averages

**Command Used:** `uptime`

**Question:**  
A developer says the server is slow. You suspect high load. How do you confirm it?

**Answer:**
```bash
uptime
```

**Explanation:**  
The load averages at the end of `uptime` output indicate the system load in the last 1, 5, and 15 minutes. High values compared to CPU cores can indicate overuse. Interviewers like candidates who can correlate performance issues with load.

---

## ✅ 3. Scenario: Check Disk Space on All Mounted Filesystems

**Command Used:** `df`

**Question:**  
How do you check disk usage on all file systems in human-readable format?

**Answer:**
```bash
df -h
```

**Explanation:**  
`df -h` gives an overview of disk usage in GB/MB. It's essential for detecting full partitions, especially `/`, `/var`, or `/home`. Commonly used in troubleshooting “disk full” errors.

---

## ✅ 4. Scenario: Check Which Directory is Taking Up Most Space

**Command Used:** `du`

**Question:**  
The `/var` partition is nearly full. How do you find out which subdirectory is using the most space?

**Answer:**
```bash
du -sh /var/* | sort -hr | head -10
```

**Explanation:**  
This command summarizes each subdirectory’s size, sorts them in human-readable format, and lists the top 10 largest. Perfect for space audits and finding logs or backups consuming storage.

---

## ✅ 5. Scenario: Check Disk Usage of Current Directory Recursively

**Command Used:** `du`

**Question:**  
You're inside a directory and want to see size of all subfolders recursively. How do you do that?

**Answer:**
```bash
du -h --max-depth=1
```

**Explanation:**  
This shows a readable breakdown of folder sizes one level deep. Very helpful when analyzing which folders are growing in size within applications, backups, or user directories.

---
```

============================================================GIT==========================================================

# **Git Questions and Answers**

This document provides detailed explanations and commands for common Git and GitHub scenarios, helping both beginners and experienced professionals.

---

## **1. Difference Between `git pull` and `git fetch`**
- **`git fetch`:** Retrieves new data from a remote repository without merging it into your working directory.
- **`git pull`:** Fetches the data and automatically merges it into your current branch.

---

## **2. Difference Between `git merge` and `git rebase`**
- **`git merge`:** Combines the histories of two branches, creating a new commit.
- **`git rebase`:** Moves or combines a sequence of commits to a new base commit, resulting in a linear history.

---

## **3. Handling Merge Conflicts**
- Git will mark the files with conflicts. Steps to resolve:
  1. Open the conflicted files and manually edit them to resolve the conflicts.
  2. Remove conflict markers (`<<<<<<`, `======`, `>>>>>>`).
  3. Mark the conflict as resolved:
     ```bash
     git add <file>
     ```
  4. Commit the merge:
     ```bash
     git commit
     ```

---

## **4. Changing the Most Recent Commit Message**
- Use:
  ```bash
  git commit --amend
  ```
- If the commit is already pushed, force-push with:
  ```bash
  git push --force
  ```

---

## **5. Reverting a Commit**
- Use:
  ```bash
  git revert <commit-id>
  ```
- This creates a new commit that undoes the changes from the specified commit.

---

## **6. Fast-Forward Merge**
- A fast-forward merge occurs when the current branch's head is directly ahead of the branch you’re merging, so no new merge commit is created.

---

## **7. `git reset --hard`**
- Resets the working directory and staging area to a specified commit, discarding all changes:
  ```bash
  git reset --hard <commit-id>
  ```

---

## **8. Undoing a Staged Commit**
- Use:
  ```bash
  git reset
  ```
- To unstage specific files:
  ```bash
  git reset <file>
  ```

---

## **9. Difference Between `git stash` and `git commit`**
- **`git stash`:** Temporarily saves uncommitted changes.
- **`git commit`:** Permanently saves changes to the local repository.

---

## **10. Undoing a `git pull`**
- Use:
  ```bash
  git reset --hard HEAD~1
  ```

---

## **11. Difference Between Git Branch and Git Tag**
- **Branch:** Tracks development of features or fixes.
- **Tag:** Marks a specific point in history (e.g., a release).

---

## **12. Creating a New Git Branch**
- To create a new branch:
  ```bash
  git branch <branch-name>
  ```
- To create and switch to the new branch:
  ```bash
  git checkout -b <branch-name>
  ```

---

## **13. Purpose of `.gitignore`**
- `.gitignore` specifies files and directories to ignore in version control.

---

## **14. Checking Modified Files**
- Use:
  ```bash
  git status
  ```

---

## **15. Pull Request in GitHub**
- A pull request is a way to propose changes to a repository on GitHub. It allows for review and discussion before merging.

---

## **16. Merging a Pull Request on GitHub**
1. Navigate to the pull request.
2. Review the changes.
3. Click the "Merge pull request" button.

---

## **17. Squashing Commits**
- Combine multiple commits into one:
  ```bash
  git rebase -i <commit-hash>
  ```
  - Change `pick` to `squash` for the commits to be squashed.

---

## **18. GitHub Fork**
- A fork creates a personal copy of a repository on GitHub for independent changes without affecting the original.

---

## **19. Difference Between `git clone` and GitHub Fork**
- **`git clone`:** Creates a local copy of a repository.
- **Fork:** Creates a personal copy of a repository on GitHub.

---

## **20. Deleting a Branch**
- **Locally:**
  ```bash
  git branch -d <branch-name>
  ```
- **Remotely:**
  ```bash
  git push origin --delete <branch-name>
  ```

---

## **21. Linking a Local Repository to a Remote Repository**
1. Create a repository on GitHub.
2. Link it to your local repository:
   ```bash
   git remote add origin <repository-url>
   git push -u origin <branch-name>
   ```

---

## **22. Difference Between `git diff` and `git status`**
- **`git diff`:** Shows changes between the working directory and staging area.
- **`git status`:** Shows the current state of the working directory and staging area.

---

## **23. Resolving Pull Request Conflicts**
- Pull the changes, resolve conflicts locally, commit the changes, and push them back to the pull request.

---

## **24. Git Submodules**
- A submodule is a Git repository inside another Git repository. It allows you to include one repository as a subdirectory.

---

## **25. Difference Between `git log` and `git reflog`**
- **`git log`:** Shows commit history.
- **`git reflog`:** Shows the history of Git references (e.g., HEAD).

---

## **26. Force Push**
- Use:
  ```bash
  git push --force
  ```
- It overwrites changes on the remote repository and should be used carefully.

---

## **27. Git Tags**
- Tags mark specific points in history, commonly used for releases:
  ```bash
  git tag <tag-name>
  ```

---

## **28. `git pull` vs. `git fetch`**
- **`git fetch`:** Retrieves remote changes but does not merge them.
- **`git pull`:** Fetches changes and merges them into the current branch.

---

## **29. Undoing the Last Commit**
- To undo the last commit but keep changes:
  ```bash
  git reset --soft HEAD~1
  ```
- To discard changes:
  ```bash
  git reset --hard HEAD~1
  ```

---

## **30. Managing Multiple Remotes**
- Add a remote:
  ```bash
  git remote add <name> <url>
  ```
- List remotes:
  ```bash
  git remote -v
  ```

---

## **Additional Git Scenarios**

### **Difference Between `git add .` and `git add *`**
- **`git add .`:** Adds all changes (new, modified, and deleted files) in the current directory and subdirectories.
- **`git add *`:** Adds changes to tracked files but does not include hidden files.

---

### **Removing Working Directory Files**
- Display files to be deleted:
  ```bash
  git clean -n
  ```
- Force delete files:
  ```bash
  git clean -f
  ```

---

### **Moving Files from Staging Area to Working Directory**
- Move all files:
  ```bash
  git reset
  ```
- Move a specific file:
  ```bash
  git reset <file>
  ```

---

### **Reverting Bad Commits**
- To revert a commit:
  ```bash
  git revert <commit-id>
  ```

---

### **Deleting Updated Code in Remote Repository**
- First, delete the code locally and then push:
  ```bash
  git push origin <branch-name>
  ```

---

### **Difference Between `git reset` and `git revert`**
- **`git reset`:** Moves changes from the staging area to the working directory.
- **`git revert`:** Creates a new commit to undo changes without altering history.

---

## **What is a `.gitignore` File?**
- A `.gitignore` file specifies files and directories to exclude from version control. Example:
  ```plaintext
  # Ignore all log files
  *.log

  # Ignore the build directory
  /build
  ```

---


**#Git #GitHub #VersionControl #DevOpsPreparation**