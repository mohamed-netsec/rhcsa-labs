## Day 1: systemd Services & journalctl Logging

### 🎯 Objectives
- Manage system services using systemctl (start, stop, enable, mask).
- Analyze boot time performance using systemd-analyze.
- Filter and inspect system logs using journalctl.

### Key Commands Executed
```bash
# Service Control & Boot Analysis
systemctl status sshd
systemd-analyze blame

# Log Filtering (RHCSA Core)
journalctl -u sshd
journalctl -b
journalctl -p err
```
## 📸 Visual Verification

### Journalctl Logs & Boot Analysis
![Boot Logs Analysis](./day1-journalctl-boot.png)
![Error Logs Verification](./day1-journalctl-err.png)
![SSHD Logs Check](./day1-journalctl-sshd.png)

### Systemctl Service Management (HTTPD)
![Enable HTTPD Service](./day1-systemctl-httpd-enable.png)
![Start HTTPD Service](./day1-systemctl-httpd-start.png)
![HTTPD Service Status](./day1-systemctl-httpd2.png)

### Target Management & Performance
![System Targets](./day1-systemctl-targets.png)
![Systemd Startup Analysis](./day1-systemctl-analyze.png)
