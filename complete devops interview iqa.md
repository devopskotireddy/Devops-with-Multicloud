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
====================================================================

1. I have 1 production server. Suddenly that server is not responding, but you are trying to SSH that server from your local. After logging in successfully, you noticed so and so disk is taking 100%, disk is full, that is the reason why system is slow. How can you resolve it?

2. I deployed an application into the server, application is not responding (as a DevOps Engineer you already having server access). I deployed that microservice, but I am not able to get my application as expected. UI is getting slow. How can you debug and troubleshoot?

3. My website `httpd` service is failing to start, that service got failed. How will you troubleshoot?

4. My `crontab` is not working. I configured properly. What can we do now?
5. People are trying to SSH the server, they entered wrong password & getting errors after multiple attempts. Those logs in /var/log/secure file.inside that file we are having logs and ip addresses, IP-Addresses is in 11th column. What are the failed SSH attempts, and how do you list only failed IPs?
6. If I delete the root directory by mistake via `rm -rf /`, how can we recover it or what will happen?

7. DevOps engineer wrote a script to delete something. How do you prevent accidental deletion?
(Example: add confirmation like `Are you sure?`)

8. We have log file and want to filter 2 errors - one is `404 error`, another is `500 internal server error`. How to get that data?

9. My disk is full. Which folder is taking the most memory? How to find which folders?

10. I am giving a string input in shell script, how to display the characters one by one?

11. In a shell script, how do you check if the user executing the script has sudo permissions or not?

12. I want to Terminate some processes, How can you do that?

13. What is the difference between soft link and hard link in Linux?

14. By mistakenly a user deletes an important file. How to recover it?

15. Can you please Explain some scenarios where did you used grep, sed and awk commands in your project?

16. Explain the Git life-cycle flow.

17. Can you please explain the Linux directory structure?

18. How can you delete a branch in remote repository from CLI?

19. Difference between `git reset` and `git revert`?

20. Explain what are the branches are there and what are the branching strategies in your project?

21. How can you delete the branch in remote repository from CLI ?

22. Difference between Git & GitHub ?

23. Explain difference between Branch & Tag, where did you used in your project ?

24. Difference between Git fetch & pull, where did you used in your project ?

25. By mistakenly i did wrong commit, How to delete that ?

26. What is your task in GitHub daily, what you will do in git on daily basis ?


27. What are the challenges you are facing daily in Git ?
# **Challenges Faced Daily in Git**

As a DevOps Engineer, working with Git on a daily basis involves several challenges, both technical and collaboration-related. Below are some common challenges and their solutions.

---

## **1. Merge Conflicts**
- **Challenge:**
  - Conflicts arise when multiple developers work on the same file or section of code and attempt to merge changes.
- **Solution:**
  - Pull changes frequently using `git pull` to stay updated.
  - Resolve conflicts manually by editing the files and removing conflict markers (`<<<<<<`, `======`, `>>>>>>`).
  - After resolving, mark the conflicts as resolved:
    ```bash
    git add <file>
    git commit
    ```

---

## **2. Accidental Commits or Pushes**
- **Challenge:**
  - Accidentally committing sensitive data or incorrect changes to the repository.
- **Solution:**
  - Undo the commit before pushing:
    ```bash
    git reset --soft HEAD~1
    ```
  - If already pushed, use:
    ```bash
    git revert <commit-id>
    git push --force
    ```

---

## **3. Branch Management**
- **Challenge:**
  - Managing multiple branches and ensuring proper branching strategies.
- **Solution:**
  - Follow a branching strategy like Git Flow:
    - **Feature Branches:** For new features.
    - **Hotfix Branches:** For critical fixes.
    - **Release Branches:** For preparing releases.
  - Use meaningful branch names like `feature/add-login` or `bugfix/fix-crash`.

---

## **4. Forgotten or Incorrect Commit Messages**
- **Challenge:**
  - Writing unclear or incorrect commit messages makes it hard to track changes.
- **Solution:**
  - Fix the last commit message using:
    ```bash
    git commit --amend
    ```
  - If already pushed, use:
    ```bash
    git push --force
    ```

---

## **5. Debugging the History**
- **Challenge:**
  - Identifying when and where a bug or issue was introduced in the codebase.
- **Solution:**
  - Use `git log` to review the commit history.
  - Use `git bisect` to isolate the commit causing the issue:
    ```bash
    git bisect start
    git bisect bad
    git bisect good <commit-id>
    ```

---

## **6. Handling Large Files**
- **Challenge:**
  - Pushing or handling large files in the repository can slow down Git operations.
- **Solution:**
  - Use `.gitignore` to exclude unnecessary files.
  - Use Git LFS (Large File Storage) for managing large files.

---

## **7. Rewriting Commit History**
- **Challenge:**
  - Rewriting history (e.g., with `git rebase`) in shared branches can cause conflicts or data loss.
- **Solution:**
  - Avoid rewriting history in shared branches.
  - Communicate with the team before performing a rebase.

---

## **8. Stale or Forgotten Branches**
- **Challenge:**
  - Accumulation of old branches clutters the repository.
- **Solution:**
  - Regularly delete merged branches:
    - Locally:
      ```bash
      git branch -d <branch-name>
      ```
    - Remotely:
      ```bash
      git push origin --delete <branch-name>
      ```

---

## **9. Code Reviews and Collaboration**
- **Challenge:**
  - Delays in code reviews and ensuring team members follow Git best practices.
- **Solution:**
  - Use pull requests for code reviews to ensure quality.
  - Automate checks with tools like GitHub Actions or CI/CD pipelines.

---

## **10. Permissions and Access Control**
- **Challenge:**
  - Ensuring team members have the right permissions to the repository.
- **Solution:**
  - Use GitHub Teams to manage permissions and enforce access control.

---

## **Real-World Example**
- **Scenario:** After merging a feature branch into `main`, the build starts failing due to a missing function.
- **Solution:**
  - Use `git log` or `git blame` to identify the problematic commit.
  - Fix the issue by reverting or applying a patch:
    ```bash
    git revert <commit-id>
    ```

---

By addressing these challenges systematically, you can ensure a smoother Git workflow and avoid common pitfalls.




28. A scheduled backup script in crontab isn’t running. How do you debug it?
answer;
Debugging a Scheduled Backup Script in Crontab
Verify Crontab Entry:

Check if the backup script is correctly scheduled.
Use the command:
bash
crontab -l
Example entry:
Code
0 2 * * * /path/to/backup_script.sh
Check Crontab Service:

Ensure the cron service is running.
bash
sudo systemctl status cron
If it’s not running, start it:
bash
sudo systemctl start cron
Check Script Permissions:

The script must be executable.
bash
chmod +x /path/to/backup_script.sh
Redirect Output to a Log File:

Update the crontab entry to capture errors:
Code
0 2 * * * /path/to/backup_script.sh > /path/to/cron.log 2>&1
After the scheduled time, check the log file:
bash
cat /path/to/cron.log
Check Cron Logs:

Look for cron job activity in system logs:
bash
sudo grep CRON /var/log/syslog
Manually Run the Script:

Run the script manually to see if it works:
bash
/path/to/backup_script.sh
Add Environment Variables (if needed):

Cron runs in a limited shell. Add paths if required:
bash
PATH=/usr/local/sbin:/usr/local/bin:/sbin:/bin:/usr/sbin:/usr/bin


Real time example:

You’ve scheduled a backup script at 2 AM, but it’s not running.
After checking, you find:
The cron service was stopped. You started it using sudo systemctl start cron.
The script had no execute permissions. You fixed it using chmod +x.
The script had missing dependencies. You added the correct PATH to the crontab.
Solution: After fixing these issues, the script ran successfully at the next scheduled time.

29. Whenever I am trying to connect my server through ssh, i am not able to connect, what might be the reason? How can you Debug ?
1. Check Network Connectivity
2. Verify SSH Service on the Server
3. Check SSH Configuration client / server side
4. Verify Firewall Rules
5. Check for IP Restrictions
6. Verify SSH Key or Password

30. I am having 1 static string, I want to revert that staric String can you please write a sample shell script?
.answer
#!/bin/bash

# Define the static string
static_string="your_static_string_here"

# Reverse the string using rev command
reversed_string=$(echo "$static_string" | rev)

# Print the reversed string
echo "Original String: $static_string"
echo "Reversed String: $reversed_string"


**#Git #GitHub #VersionControl #DevOpsPreparation**