# **Linux Advanced Topics: Storage Management**

Storage management is a critical skill for Linux professionals, especially in roles like DevOps, System Administration, and Cloud Engineering. This guide provides a deep dive into advanced Linux storage concepts, commands, and real-world scenarios to help you ace interviews.

---

## **1. Partition Management**

### **1.1. Creating and Managing Partitions**
- **Commands:**
  ```bash
  sudo fdisk /dev/sdX   # Enter interactive partitioning mode
  ```
  - `n`: Create a new partition.
  - `w`: Write changes to the disk.
  - `p`: Print the partition table.

- **Scenario:**
  A new disk `/dev/sdb` is added to your server. You need to create a partition for a new application.
  ```bash
  sudo fdisk /dev/sdb
  ```

### **1.2. Viewing Partition Information**
- **Command:**
  ```bash
  lsblk
  ```
- **Explanation:**
  - Lists all block devices with their mount points.

---

## **2. Filesystem Management**

### **2.1. Formatting Partitions**
- **Command:**
  ```bash
  sudo mkfs.ext4 /dev/sdX1
  ```
- **Scenario:**
  After creating a partition `/dev/sdb1`, you need to format it with the `ext4` filesystem.

### **2.2. Mounting Filesystems**
- **Command:**
  ```bash
  sudo mkdir /mnt/storage
  sudo mount /dev/sdb1 /mnt/storage
  ```
- **Scenario:**
  Mount the partition `/dev/sdb1` to `/mnt/storage` for use.

### **2.3. Persisting Mounts**
- **Edit `/etc/fstab`:**
  ```bash
  sudo nano /etc/fstab
  ```
  - Add an entry:
    ```
    /dev/sdb1  /mnt/storage  ext4  defaults  0  2
    ```
- **Scenario:**
  Ensure that a storage partition is automatically mounted after a system reboot.

---

## **3. Logical Volume Management (LVM)**

### **3.1. Creating LVM**
1. **Initialize Physical Volume (PV):**
   ```bash
   sudo pvcreate /dev/sdb
   ```
2. **Create a Volume Group (VG):**
   ```bash
   sudo vgcreate my_vg /dev/sdb
   ```
3. **Create a Logical Volume (LV):**
   ```bash
   sudo lvcreate -L 10G -n my_lv my_vg
   ```

### **3.2. Extending Logical Volumes**
- **Command:**
  ```bash
  sudo lvextend -L +5G /dev/my_vg/my_lv
  sudo resize2fs /dev/my_vg/my_lv
  ```
- **Scenario:**
  Your application running on `/dev/my_vg/my_lv` needs more storage. Extend the logical volume by 5GB.

---

## **4. Disk Monitoring and Management**

### **4.1. Disk Space Usage**
- **Command:**
  ```bash
  df -h
  ```
- **Scenario:**
  Check available and used disk space on all mounted filesystems.

### **4.2. Disk Usage by Directory**
- **Command:**
  ```bash
  du -sh /path/to/directory
  ```
- **Scenario:**
  Identify directories consuming the most disk space.

### **4.3. Disk I/O Monitoring**
- **Command:**
  ```bash
  iostat -x 1
  ```
- **Scenario:**
  Monitor disk I/O to troubleshoot performance issues.

---

## **5. RAID (Redundant Array of Independent Disks)**

### **5.1. Creating a RAID 0 (Striping)**
- **Command:**
  ```bash
  sudo mdadm --create /dev/md0 --level=0 --raid-devices=2 /dev/sdb /dev/sdc
  ```

### **5.2. Monitoring RAID**
- **Command:**
  ```bash
  cat /proc/mdstat
  ```
- **Scenario:**
  Set up a RAID array for improved performance or redundancy and monitor its status.

---

## **6. Backup and Recovery**

### **6.1. Creating Backups**
- **Command:**
  ```bash
  tar -czvf backup.tar.gz /path/to/directory
  ```

### **6.2. Restoring Backups**
- **Command:**
  ```bash
  tar -xzvf backup.tar.gz -C /restore_path
  ```

### **6.3. Using `rsync` for Incremental Backups**
- **Command:**
  ```bash
  rsync -av /source/path /backup/path
  ```
- **Scenario:**
  Automate daily backups using `rsync`.

---

## **7. Network Storage (NFS and iSCSI)**

### **7.1. Setting Up NFS Server**
- **Commands:**
  1. Install NFS:
     ```bash
     sudo apt install nfs-kernel-server
     ```
  2. Configure `/etc/exports`:
     ```
     /shared/folder 192.168.1.0/24(rw,sync,no_root_squash)
     ```
  3. Restart NFS service:
     ```bash
     sudo systemctl restart nfs-kernel-server
     ```

### **7.2. Mounting NFS Share on Client**
- **Command:**
  ```bash
  sudo mount 192.168.1.100:/shared/folder /mnt/nfs
  ```

### **7.3. Setting Up iSCSI**
- **Commands:**
  1. Install iSCSI Initiator:
     ```bash
     sudo apt install open-iscsi
     ```
  2. Discover Targets:
     ```bash
     sudo iscsiadm -m discovery -t sendtargets -p <iSCSI_Target_IP>
     ```

---

## **8. Real-Time Scenarios**

### **Scenario 1: Adding a New Disk**
- A new disk `/dev/sdb` is added to the server. Format it, create a mount point `/mnt/data`, and ensure it persists across reboots.
  - Solution:
    ```bash
    sudo mkfs.ext4 /dev/sdb
    sudo mkdir /mnt/data
    sudo mount /dev/sdb /mnt/data
    echo "/dev/sdb /mnt/data ext4 defaults 0 2" | sudo tee -a /etc/fstab
    ```

### **Scenario 2: Fixing a Full Disk**
- Your `/var` directory is running out of space. Move it to a new disk `/dev/sdb1`.
  - Solution:
    ```bash
    sudo rsync -av /var /mnt/new_disk/
    sudo mv /var /var_old
    sudo ln -s /mnt/new_disk/var /var
    ```

### **Scenario 3: Expanding Storage for a Live Application**
- Your application on `/dev/my_vg/my_lv` requires more storage urgently.
  - Solution:
    ```bash
    sudo lvextend -L +10G /dev/my_vg/my_lv
    sudo resize2fs /dev/my_vg/my_lv
    ```

---

## **Key Takeaways**
1. Master partitioning, formatting, and mounting for basic storage tasks.
2. Use LVM for flexible and scalable storage management.
3. Monitor disk usage and I/O to troubleshoot performance issues.
4. Implement RAID for redundancy and performance.
5. Automate backups with `rsync` and `tar`.
6. Explore network storage solutions like NFS and iSCSI for scalable environments.

---

*Prepared for students and professionals by **Kotireddy*** 🚀  
**#Linux #StorageManagement #AdvancedTopics #DevOps #SystemAdministration**