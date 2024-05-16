## Step-by-Step Guide
<details>
<summary><b>1. Nginx Setup for `www.abc.com` with SSL</b></summary>

#### 1. Update the package list and install Nginx:
```
sudo apt update
sudo apt install nginx
```

#### 2. Create Nginx Configuration for www.abc.com

```
sudo nano /etc/nginx/sites-available/www.abc.com
```

#### 3. Add the following content to the file:

```
server {
    listen 80;
    server_name www.abc.com;

    location / {
        proxy_pass http://localhost:3000;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}

```

#### 3. Create a symbolic link to enable the configuration:
```
sudo ln -s /etc/nginx/sites-available/www.abc.com /etc/nginx/sites-enabled/
```

#### 4. Test Nginx Configuration

```
sudo nginx -t
```

#### 5. Reload Nginx to apply the changes:

```
sudo systemctl reload nginx
```

#### 6. Install Certbot and Obtain SSL Certificate

```
sudo apt install certbot python3-certbot-nginx
```

#### 7. Obtain the SSL certificate for www.abc.com:

```
sudo certbot --nginx -d www.abc.com
```

#### 8. Verify SSL Configuration
```
cat /etc/nginx/sites-available/www.abc.com
```

#### 9. Test Nginx Configuration Again

```
sudo nginx -t
```

#### 10. Reload Nginx
```
sudo systemctl reload nginx
```
## Optional
10. Auto-Renew the Certificate
```    
sudo certbot renew --dry-run
```

</details>

<details>
<summary><b>1. Nginx Setup for `www.abc.com` with SSL</b></summary>
