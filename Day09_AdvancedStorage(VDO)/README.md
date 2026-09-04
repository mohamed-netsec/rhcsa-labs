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

Step 4: Persistent Mounting Configuration
Configure /etc/fstab for persistent mounting across system reboots:

/dev/vg-vdo/lv-vdo    /data/vdo-storage    ext4    defaults    0 0


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
