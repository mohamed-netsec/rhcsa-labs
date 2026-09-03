### Dayo08 SwapFiles in linux

### 1.Create Swap File
```Bash
sudo dd if=/dev/zero of=/swapfile bs=1M count=1024
sudo chmod 600 /swapfile
sudo mkswap /swapfile
sudo swapon /swapfile
swapon --show
```
### 2.Persistent (fstab):
```Bash
sudo nano /etc/fstab
# add the line:
/swapfile   none   swap   defaults   0   0
```
### 3.Delete Swap File
```Bash
sudo swapoff -v /swapfile
sudo rm /swapfile
sudo nano /etc/fstab   # remove the /swapfile line
```
