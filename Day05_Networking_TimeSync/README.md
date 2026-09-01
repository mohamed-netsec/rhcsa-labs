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
![Hostname Configuration](./hostname.png)

### 2. Network & IP Verification Snapshots
![nmcli Configuration](./nmcli-config.png)
![IP Address Details](./ip-a.png)

### 3. Time Synchronization Snapshots
![Timezone and Chrony Status](./timedatectl-chrony.png)
![Chrony Sources Verification](./chrony.png)

### 4. Firewall Verification Snapshot
![Firewall NTP Service](./firewall-cmd.png)


