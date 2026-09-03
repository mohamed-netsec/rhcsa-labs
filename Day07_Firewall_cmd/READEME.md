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
