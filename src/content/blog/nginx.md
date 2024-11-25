---
author: Tien Nguyen
pubDatetime: 2024-11-25T17:11:85
modDatetime: 2024-11-25T17:11:85
title: Nginx notes
slug: nginx-notes
featured: true
draft: false
tags:
  - docs
  - devops
  - nginx
  - trick
description: Nginx notes
---

- Whitelist IP
```nginx
server {
    listen 80;
    listen [::]:80;

    server_name _;

    error_log  /var/log/nginx/error.log;
    access_log /var/log/nginx/access.log;

    allow x.x.x.x;
    allow y.y.y.y;
    deny all;

    location / {
        root /var/www/html;
    }
}
```

- Show list file in folder
```nginx
server {
    listen 80;
    listen [::]:80;

    server_name ;

    error_log  /var/log/nginx/error.log;
    access_log /var/log/nginx/access.log;

    location / {
        root /files;
        autoindex on;
        autoindex_exact_size off;
        autoindex_format html;
        autoindex_localtime on;
    }
}
```

- Set real ip in nginx ( through cloudflare )
```nginx
server {
    listen 80;
    listen [::]:80;

    server_name _;

    error_log  /var/log/nginx/error.log;
    access_log /var/log/nginx/access.log;

    location = /robots.txt {
        alias /etc/nginx/conf.d/robots.txt;
    }

    # set real ip from cloudflare
    set_real_ip_from 0.0.0.0/0;
    real_ip_header X-Forwarded-For;
    real_ip_recursive on;

    location / {
        root /var/www/html;
    }
}
```