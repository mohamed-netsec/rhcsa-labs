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
