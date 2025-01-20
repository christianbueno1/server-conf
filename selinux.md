## fedora server
```
# Option 1: Set SELinux Boolean for Nginx
# Allow Nginx to Connect to Network:
sudo setsebool -P httpd_can_network_connect 1
#sudo setsebool -P httpd_can_network_connect true

# Restart Nginx:
sudo systemctl restart nginx
```

## SELinux
### Understanding the Issue
1. SELinux Enforcing Mode:
    - In enforcing mode, SELinux policies are strictly enforced, which can prevent Nginx from connecting to Jenkins if the policies do not allow it.
    - The error message in the logs may indicate that Nginx is being denied access when trying to connect to the Jenkins service.
2. Permissive Mode:
    - When you set SELinux to permissive mode using setenforce permissive, it allows all operations but logs any denials. This is why the 502 error goes away; Nginx can connect to Jenkins without restrictions.