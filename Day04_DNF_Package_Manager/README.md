# 📦 Day 4: Package Management using DNF

# 🎯 Objectives
* Master package search and detailed inspection using dnf.
* Install and verify packages (such as nginx) on RHEL.
* Identify package providers for specific configuration files using dnf provides.
* Remove packages safely using the dnf package manager.
---

## 🛠️ Executed Commands & Operations

### 1. Package Search & Inspection
`bash
# Search for nginx package details and configuration provider
dnf search nginx
dnf info nginx
dnf provides /etc/nginx/nginx.conf
# Install nginx web server package
sudo dnf install -y nginx

# Verify installed package
dnf list installed | grep nginx
# Remove package from the system
sudo dnf remove -y nginx
📸 Visual Verification
## 📸 Visual Verification

![Package Installation](./day4-dnf-install.png)
![Package Listing & Verification](./day4-dnf-list.png)
![File Provider Tracking](./day4-dnf-provides.png)
![Package Removal](./day4-dnf-remove.png)
