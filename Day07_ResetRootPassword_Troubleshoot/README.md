Resetting Root Password on RHEL 10
Recovering a lost root password by booting into emergency shell and updating filesystem permissions.
### Step-by-Step Recovery

# 1.Interrupt Boot Process:

Restart system, press e on the GRUB menu line.
Append ```init=/bin/bash``` to the linux line, then press Ctrl + X.

# 2. Remount & Change Password :
```
mount -o remount,rw /
passwd 
```
# 3.Enable SELinux Relabeling & Reboot:
```
touch /.autorelabel
exec /sbin/init
```
