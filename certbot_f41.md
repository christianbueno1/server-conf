## certbot
```
sudo dnf install certbot python3-certbot-nginx

# obtain an SSL certificate
sudo certbot --nginx -d jenkins.christianbueno.me

# after successful installation, you can verify the configuration
# go to cloudflare and change the SSL/TLS encryption mode to Full (strict)

# test
curl -I https://jenkins.christianbueno.me

# list certificates
sudo certbot certificates


```