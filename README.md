# Simple static website hosting on Ubuntu VM

## Simple static website code files are index.html, style.css & script.js

## Deploy it on your VM with Nginx

```
sudo apt update
sudo apt install nginx -y
```

**Create the website directory:**

```
sudo mkdir -p /var/www/devops-site
```

**Copy your three files there:**

```
/var/www/devops-site/
├── index.html
├── style.css
└── script.js
```

**Set ownership:**

```
sudo chown -R www-data:www-data /var/www/devops-site
```

**Create an Nginx configuration:**

```
vim nano /etc/nginx/sites-available/devops-site
```

**Put Code as below :**

```
server {
    listen 80;
    listen [::]:80;

    server_name _;

    root /var/www/devops-site;

    index index.html;

    location / {
        try_files $uri $uri/ =404;
    }
}
```

**Enable it:**

```
sudo ln -s /etc/nginx/sites-available/devops-site \
/etc/nginx/sites-enabled/devops-site
```

**Remove the default site:**

```
sudo rm /etc/nginx/sites-enabled/default
```

**Test the configuration:**

```
sudo nginx -t
```

**If you get:**

```
syntax is ok
test is successful
```

**restart Nginx:**

```
sudo systemctl restart nginx
sudo systemctl enable nginx
```

