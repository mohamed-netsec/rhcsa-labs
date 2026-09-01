## Day 2: LVM Basics & Storage Management

### 🎯 Objectives
- Create Physical Volumes (PV), Volume Groups (VG), and Logical Volumes (LV).
- Format LVs with ext4 and configure persistent mounting via /etc/fstab.
- Perform Live Expansion (lvextend).
- Clean up LVM components safely.

### Commands Executed

# 1. Physical & Volume Group Creation
```bash
pvcreate /dev/nvme0n2
vgcreate test-vg /dev/nvme0n2
```

# 2. Logical Volume Creation & Formatting
```bash
lvcreate -L 2G -n test-lv test-vg
mkfs.ext4 /dev/test-vg/test-lv
mkdir /test-data
mount /dev/test-vg/test-lv /test-data
```

# 3. Expansion & Full Cleanup
```bash
lvextend -L 4G -r /dev/test-vg/test-lv
umount -l /test-data
lvremove -f /dev/test-vg/test-lv
vgremove test-vg
pvremove /dev/nvme0n2
```
### Visual Verification
![pvcreate](./day2-pvcreate.png)
![vgcreate](./day2-vgcreate.png)
![lvcreate](./day2-lvcreate.png)
![mkfs ext4](./day2-mkfs-ext4.png)
![mount](./day2-mount.png)
![mount2](./day2-mount2.png)
![lvextend](./day2-lvextend.png)
![lvreduce](./day2-lvreduce.png)
![cleanup](./day2-cleanup.png)
