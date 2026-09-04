# RHCSA Preparation Labs (EX200)

## 📦 Day 1: systemd Services & journalctl Logging

### 📌 Objectives
- Manage system services using systemctl (start, stop, enable, disable, mask, unmask).
- Analyze boot time performance using systemd-analyze.
- Filter and inspect system logs using journalctl.

### Commands Executed
```bash
# Service Control & Boot Analysis
systemctl status httpd
systemctl start httpd
systemctl enable httpd 
systemctl is-enabled httpd
systemctl is-active httpd
systemd-analyze blame

# Log Filtering (RHCSA Core)
journalctl -u sshd
journalctl -b
journalctl -p err

```
### Visual Verification
![journalctl boot](./Day01_Systemd_Service-Manager/day1-journalctl-boot.png)
![journalctl err](./Day01_Systemd_Service-Manager/day1-journalctl-err.png)
![journalctl sshd](./Day01_Systemd_Service-Manager/day1-journalctl-sshd.png)
![systemctl enable](./Day01_Systemd_Service-Manager/day1-systemctl-httpd-enable.png)
![systemctl start](./Day01_Systemd_Service-Manager/day1-systemctl-httpd-start.png)
![systemctl status](./Day01_Systemd_Service-Manager/day1-systemctl-httpd2.png)
![systemctl targets](./Day01_Systemd_Service-Manager/day1-systemctl-targets.png)
![systemd analyze](./Day01_Systemd_Service-Manager/day1-systemd-analyze.png)
## 📦 Day 2: LVM Basics & Storage Management

### 📌 Objectives
- Create Physical Volumes (PV), Volume Groups (VG), and Logical Volumes (LV).
- Format LVs with ext4 and configure persistent mounting via /etc/fstab.
- Perform Live Expansion (lvextend).
- Clean up LVM components safely.

### Commands Executed
```bash
# 1. Physical & Volume Group Creation
pvcreate /dev/nvme0n2
vgcreate test-vg /dev/nvme0n2

# 2. Logical Volume Creation & Formatting
lvcreate -L 2G -n test-lv test-vg
mkfs.ext4 /dev/test-vg/test-lv
mkdir /test-data
mount /dev/test-vg/test-lv /test-data

# 3. Expansion & Full Cleanup
lvextend -L 4G -r /dev/test-vg/test-lv
umount -l /test-data
lvremove -f /dev/test-vg/test-lv
vgremove test-vg
pvremove /dev/nvme0n2
```
### Visual Verification
![pvcreate](./Day02_LVM_Storage/day2-pvcreate.png)
![vgcreate](./Day02_LVM_Storage/day2-vgcreate.png)
![lvcreate](./Day02_LVM_Storage/day2-lvcreate.png)
![mkfs ext4](./Day02_LVM_Storage/day2-mkfs-ext4.png)
![mount](./Day02_LVM_Storage/day2-mount.png)
![mount2](./Day02_LVM_Storage/day2-mount2.png)
![lvextend](./Day02_LVM_Storage/day2-lvextend.png)
![lvreduce](./Day02_LVM_Storage/day2-lvreduce.png)
![cleanup](./Day02_LVM_Storage/day2-cleanup.png)


## 📦 Day 3: User & Group Management, Permissions & ACLs

### 📌 Objectives
* Perform local user account creation, group assignment, and password management.
* Manage group creation, renaming, and deletion.
* Configure directory ownership, special permissions (SGID), and ACLs.

---

### Task Breakdown & Commands

1. User Management & Primary Group Assignment:
   Created user1 with a home directory, verified its identity, created a primary group Security, and set the user's password.
   ```bash
   sudo useradd -m user1
   ls /home
   id user1
   sudo groupadd Security
   sudo usermod -g Security user1
   id user1
   sudo passwd user1

2. Group Operations:
Demonstrated group creation, renaming (DevOps to Sec), and deleting redundant groups.   
```
sudo groupadd DevOps
sudo groupmod -n Sec DevOps
sudo groupdel Sec
```
3. Directory Ownership & SGID Configuration:
Created /data/project, assigned group ownership to devops, and applied the SGID bit (2770) so new files inherit the group identity.

```bash
sudo mkdir -p /data/project
sudo chown -R root:devops /data/project
sudo chmod 2770 /data/project
```
4. Access Control Lists (ACL):
Configured granular read and execute permissions (r-x) for otheruser using setfacl.

```bash
sudo setfacl -m u:otheruser:rx /data/project
getfacl /data/project
```
### Visual Verification

* **User Management (useradd, usermod, passwd):**
  ![User Management](./Day03_Users_Groups_ACLs/day3-users.png)
  ![User Management](./Day03_Users_Groups_ACLs/day3-users2.png)
  ![User Management](./Day03_Users_Groups_ACLs/day3-users3.png)

* **Group Management (groupadd, groupmod, groupdel):**
  ![Group Management](./Day03_Users_Groups_ACLs/day3-groups.png)

* **SGID & ACLs Configuration (chmod 2770, setfacl):**
  ![SGID & ACL Configuration](./Day03_Users_Groups_ACLs/day3-sgid-acls.png)

# 📦 Day 4: Package Management using DNF

## 🎯 Objectives
* Master package search and detailed inspection using dnf.
* Install and verify packages (such as nginx) on RHEL.
* Identify package providers for specific configuration files using dnf provides.
* Remove packages safely using the dnf package manager.

---

## 🛠️ Executed Commands & Operations

### 1. Package Search & Inspection
# Search for nginx package details and configuration provider
```bash
dnf search nginx
dnf info nginx
dnf provides /etc/nginx/nginx.conf  
```
### 2. Package Installation & Verification 
# Install nginx web server package
```bash
sudo dnf install -y nginx
```
# Verify installed package
```bash
dnf list installed | grep nginx
```
### 3. Package Removal
# Remove package from the system
```bash
sudo dnf remove -y nginx
```

## 📸 Visual Verification

![Package Installation](./Day04_DNF_Package_Manager/day4-dnf-install.png)
![Package Listing & Verification](./Day04_DNF_Package_Manager/day4-dnf-list.png)
![File Provider Tracking](./Day04_DNF_Package_Manager/day4-dnf-provides.png)
![Package Removal](./Day04_DNF_Package_Manager/day4-dnf-remove.png)

## Day 05: Networking, Time Synchronization & Firewalld Configuration

### 1. System Identification & Environment
- Hostname: mohamed-server
- OS: Red Hat Enterprise Linux 10.0 (Coughlan)
- Kernel: Linux 6.12.0-55.9.1.el10_0.x86_64
- Hypervisor: VMware, Inc.

### 2. Network Configuration
- Interface Name: ens160
- IP Address: 192.168.1.100/24
- Subnet Mask: 255.255.255.0
- Broadcast Address: 192.168.1.255
- MAC Address: 00:0c:29:27:b1:2a

### Commands Executed: 
  ```bash
  sudo nmcli con mod ens160 ipv4.addresses 192.168.1.100/24 ipv4.method manual
  sudo nmcli con up ens160
  ```
### 3. Time Synchronization & System Time
Timezone Set: Africa/Algiers (Set via timedatectl)
Time Daemon: chronyd installed and enabled via systemctl.
NTP Verification: Verified active time synchronization using chronyc sources -v and chronyc tracking.

### 4. Firewall Configurations
## Commands Executed
```bash
sudo firewall-cmd --add-service=ntp --permanent
sudo firewall-cmd --reload
sudo firewall-cmd --list-services
```
### Verification Summary
### 1. Hostname Verification Snapshot
![Hostname Configuration](./Day05_Networking_TimeSync/hostname.png)

### 2. Network & IP Verification Snapshots
![nmcli Configuration](./Day05_Networking_TimeSync/nmcli-config.png)
![IP Address Details](./Day05_Networking_TimeSync/ip-a.png)

### 3. Time Synchronization Snapshots
![Timezone and Chrony Status](./Day05_Networking_TimeSync/timedatectl-chrony.png)
![Chrony Sources Verification](./Day05_Networking_TimeSync/chrony.png)

### 4. Firewall Verification Snapshot
![Firewall NTP Service](./Day05_Networking_TimeSync/firewall-cmd.png)


### DAY06
### RHCSA SELinux Practice: Custom Web Root & Non-Standard Port Configuration
#  🎯 Overview
This repository contains a step-by-step practical implementation for configuring a custom web server directory and non-standard HTTP port on Red Hat Enterprise Linux (RHEL) using SELinux policy management tools.
### Objectives
 -Set up a custom document root directory (/web/secure).
 -Reconfigure Apache (httpd) to run on a non-standard port (8282).
 -Apply persistent SELinux file context rules and network port labeling.
 -Enable user home directory web access via SELinux Booleans.
 
### Commands Execution Summary
# 1.Create Web Content Directory & Sample File:

```bash
mkdir -p /web/secure
echo "RHCSA TEST PAGE" > /web/secure/index.html
```
# 2.Configure Persistent SELinux File Context :

```bash
semanage fcontext -a -t httpd_sys_content_t "/web/secure(/.*)?"
restorecon -Rv /web/secure
```

# 3. Update Apache Configuration : (/etc/httpd/conf/httpd.conf)
Change Listen 80 to Listen 8282.
Update DocumentRoot and <Directory> block to /web/secure.

# 4. Add Custom Port to SELinux Policy :
```
semanage port -a -t http_port_t -p tcp 8282
```
# 5. Enable SELinux Home Directory Label :
```
setsebool -P httpd_enable_homedirs on
```

# 6. Restart Service & Verification : 
```
systemctl restart httpd
curl http://localhost:8282
```
### Troubleshooting Notes ###
​Invalid Port Type Error: When executing semanage port, use http_port_t instead of httpd_port_t.
​File Context Application: Remember to execute restorecon after semanage fcontext to apply context labeling to existing files on disk.


### Day07 : Firewalld Management: Port & Advanced Rich Rules Configuration

# 🎯 Objectives :
-Manage active zone configurations (public).
-Allow standard web services (http) and non-standard custom ports (8282/tcp).
-Implement Firewalld Rich Rules for conditional traffic control based on source IP addresses.
-Persist and apply runtime firewall updates.

## Commands Executed :
# 1.Standard service and custom port : 
```
firewall-cmd --add-service=http --permanent
firewall-cmd --add-port=8282/tcp --permanent
```
# 2. HTTP drop rule configs :
```
firewall-cmd --add-rich-rule='rule family="ipv4" source address="10.0.0.5" service name="http" drop' --permanent
```
# 3. Advanced SSH traffic control :
```
irewall-cmd --add-rich-rule='rule family="ipv4" source address="192.168.1.55" service name="ssh" drop' --permanent
firewall-cmd --add-rich-rule='rule family="ipv4" source address="192.168.1.55" service name="ssh" accept' --permanent
```
# 4. Reload configs & Verification :
```
firewall-cmd --reload
firewall-cmd --list-all
firewall-cmd --list-rich-rules
```

### Dayo08 SwapFiles in linux

### 1.Create Swap File
```Bash
sudo dd if=/dev/zero of=/swapfile bs=1M count=1024
sudo chmod 600 /swapfile
sudo mkswap /swapfile
sudo swapon /swapfile
swapon --show
```
![Create](./Day08_Swapfiles/1.png)

### 2.Persistent (fstab):
```Bash
sudo nano /etc/fstab
# add the line:
/swapfile   none   swap   defaults   0   0
```
![fstab](./Day08_Swapfiles/2.png)

### 3.Delete Swap File
```Bash
sudo swapoff -v /swapfile
sudo rm /swapfile
sudo nano /etc/fstab   # remove the /swapfile line
```
![delete](./Day08_Swapfiles/3.png)


# Day 09: Advanced Storage Implementation - VDO (Virtual Data Optimizer) on RHEL 10

## 📌 Overview
This lab demonstrates the deployment and configuration of Virtual Data Optimizer (VDO) via LVM on Red Hat Enterprise Linux 10 (RHEL 10). VDO provides inline data reduction through Zero-block Elimination, Deduplication, and Compression, optimizing storage utilization for enterprise workloads.

---

## 🛠️ Environment & Technical Specifications
* OS: Red Hat Enterprise Linux 10 (RHEL 10)
* Physical Target Disk: /dev/nvme0n2 (10 GB)
* Volume Group (VG): vg-vdo
* Logical Volume (LV): lv-vdo
* **Physical LV Allocation (-L):** 5 GB
* **Virtual LV Provisioning (-V):** Filesystem:ystem:** ext4
* **Mount Point:** /data/vdo-storage

---

## 🚀 Step-by-Step Implementation

### Step 1: Storage Layer Initialization
Initialize the physical volume and create the dedicated LVM volume group on the NVMe drive:

```bash
pvcreate /dev/nvme0n2
vgcreate vg-vdo /dev/nvme0n2
```

Step 2: Native LVM VDO Provisioning
Provision a VDO-enabled logical volume using LVM native Integration (--type vdo). A 20GB virtual volume is presented to the system backed by 5GB of physical allocation:
```
vcreate --type vdo -n lv-vdo -L 5G -V 20G vg-vdo
```

Step 3: Filesystem Formatting & Mount Setup
Format the VDO logical volume with the ext4 filesystem and prepare the mount directory:
```
mkfs.ext4 /dev/vg-vdo/lv-vdo
mkdir -p /data/vdo-storage
```

![Photo](./Day09_AdvancedStorage(VDO)/1.png)

Step 4: Persistent Mounting Configuration
Configure /etc/fstab for persistent mounting across system reboots:

/dev/vg-vdo/lv-vdo    /data/vdo-storage    ext4    defaults    0 0


![fstab](./Day09_AdvancedStorage(VDO)/2.png)

Apply systemd re-configuration and mount the volume:
```
systemctl daemon-reload
mount -a
```
📊 Verification & Status Monitoring
Check Filesystem Usage
Verify that the operating system reports the 20GB virtual capacity at /data/vdo-storage:
```
df -h /data/vdo-storage
```
Verify VDO Deduplication & Compression Metrics
Inspect VDO pool operational statistics and space saving raèèètio:
```
vdostats --human-readable
```

![test](./Day09_AdvancedStorage(VDO)/3.png)
![test2](./Day09_AdvancedStorage(VDO)/4.png)




