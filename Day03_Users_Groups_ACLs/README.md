## Day 3: User & Group Management, Permissions & ACLs

### 🎯 Objectives
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
   ```
### Group Operations:
Demonstrated group creation, renaming (Sec to DevOps), and deleting redundant groups.
```bash
sudo groupadd DevOps
sudo groupmod -n Sec DevOps
sudo groupdel Sec
Directory Ownership & SGID Configuration:
Created /data/project, assigned group ownership to devops, and applied the SGID bit (2770) so new files inherit the group identity.
sudo mkdir -p /data/project
sudo chown -R root:devops /data/project
sudo chmod 2770 /data/project
```
### Access Control Lists (ACL):
Configured granular read and execute permissions (r-x) for otheruser using setfacl.
```bash
sudo setfacl -m u:otheruser:rx /data/project
getfacl /data/project
```
# User Management (useradd, usermod, passwd):
# Group Management (groupadd, groupmod, groupdel):
# SGID Configuration (chmod 2770):
# ACL Verification (getfacl):

### Visual Verification

* **User Management (useradd, usermod, passwd):**
  ![User Management](./day3-users.png)
  ![User Management](./day3-users2.png)
  ![User Management](./day3-users3.png)

* **Group Management (groupadd, groupmod, groupdel):**
  ![Group Management](./day3-groups.png)

* **SGID & ACLs Configuration (chmod 2770):**
  ![SGID Configuration](./day3-sgid-acls.png)
  
