## Installation
```
sudo dnf install vim-enhanced wget htop git
```

## jenkins
```
# jenkins version 2.479.3 LTS
sudo dnf install fontconfig java-21-openjdk

# listen
ss -antpl | grep 8080

# retrieve initial admin password
sudo cat /var/lib/jenkins/secrets/initialAdminPassword

doctl compute reserved-ip list

# 4. Check Jenkins Logs
sudo journalctl -u jenkins


```

## nginx
- [nginx reverse proxy](https://www.jenkins.io/doc/book/system-administration/reverse-proxy-configuration-with-jenkins/reverse-proxy-configuration-nginx/)
- replace server_name with your domain name
- On fedora based distro in server block replace root value with `/var/cache/jenkins/war/;`
```
sudo dnf install nginx
sudo systemctl start nginx
sudo systemctl enable nginx
sudo systemctl status nginx

ll /etc/nginx/nginx.conf
cat /etc/nginx/nginx.conf
# reverse proxy
# you do not need to remove the default server block
# but you do have to delete the default location block

# list nginx sites-available
ll /etc/nginx/conf.d/
# Add jenkins.conf file to /etc/nginx/conf.d/
sudo vim /etc/nginx/conf.d/jenkins.conf

# log jenkins
ll /var/log/nginx
# create jenkins folder
sudo mkdir /var/log/nginx/jenkins


nginx -t
nginx -T
sudo systemctl restart nginx
```

## firewall
```
sudo dnf install firewalld
sudo systemctl enable firewalld
sudo systemctl start firewalld

sudo firewall-cmd --zone=public --add-service=http --permanent
sudo firewall-cmd --zone=public --add-service=https --permanent
sudo firewall-cmd --reload

# Jenkins
YOURPORT=8080
PERM="--permanent"
SERV="$PERM --service=jenkins"

firewall-cmd $PERM --new-service=jenkins
firewall-cmd $SERV --set-short="Jenkins ports"
firewall-cmd $SERV --set-description="Jenkins port exceptions"
firewall-cmd $SERV --add-port=$YOURPORT/tcp
firewall-cmd $PERM --add-service=jenkins
firewall-cmd --zone=public --add-service=http --permanent
firewall-cmd --reload

# open port 8080
sudo firewall-cmd --add-port=8080/tcp --permanent
sudo firewall-cmd --reload

# check firewall
firewall-cmd --list-all
```

## zsh
```
sudo dnf install zsh
echo $ZSH_VERSION
echo $SHELL

```

## SELinux
```
# check status
sestatus
getenforce

# temporarily permissive
setenforce permissive
# temporarily enforcing
setenforce enforcing

# change to permisive mode permanently
sudo vim /etc/selinux/config
SELINUX=permissive
# reboot

# Set SELinux Boolean for Nginx
sudo setsebool -P httpd_can_network_connect 1

```

## Groups
```
# add user nginx to jenkins group
usermod -aG jenkins nginx
groups nginx

# remove user nginx from jenkins group
gpasswd -d nginx jenkins

```