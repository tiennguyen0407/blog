---
author: Tien Nguyen
pubDatetime: 2024-11-25
modDatetime: 2024-11-25
title: Minio notes
slug: minio-notes
featured: true
draft: false
tags:
  - docs
  - devops
  - minio
  - trick
description: Minio notes
---

- docker-compose.yaml
```yaml
services:
  minio:
    image: quay.io/minio/minio
    container_name: minio
    ports:
      - "9000:9000"
      - "9001:9001"
    environment:
      MINIO_ROOT_USER: admin
      MINIO_ROOT_PASSWORD: NhRPgfsHoT4MuDerEnLN
      MINIO_USERNAME: ubuntu
      MINIO_GROUPNAME: ubuntu
    volumes:
      - /mnt/pdf:/data
    command: server /data --console-address ":9001"
  nginx:
    image: nginx:1.27.2
    container_name: nginx
    ports:
      - "83:83"
    volumes:
      - ./nginx.conf:/etc/nginx/conf.d/default.conf
      - ./robots.txt:/etc/nginx/conf.d/robots.txt
```

- Nginx conf ( Optional )
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

    ignore_invalid_headers off;
    client_max_body_size 0;
    proxy_buffering off;
    proxy_request_buffering off;

    # # set real ip from cloudflare
    # set_real_ip_from 0.0.0.0/0;
    # real_ip_header X-Forwarded-For;
    # real_ip_recursive on;

    location / {

        allow x.x.x.x;
        allow y.y.y.y;
        deny all;

        proxy_set_header Host $http_host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
        proxy_set_header X-NginX-Proxy true;

        real_ip_header X-Real-IP;

        proxy_connect_timeout 300;

        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "upgrade";
        chunked_transfer_encoding off;
        proxy_read_timeout 86400;

        proxy_pass http://minio:9001;
    }
}
```