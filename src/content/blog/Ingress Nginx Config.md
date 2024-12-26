---
author: Tien Nguyen
pubDatetime: 2024-12-26
modDatetime: 2024-12-26
title: Ingress Nginx config
slug: ingress-nginx-config
featured: true
draft: false
tags:
  - docs
  - k8s
  - ingress
  - nginx
  - trick
description: Blog
---
- Ignore all CSP ( only ignore for test )
```nginx
Content-Security-Policy "default-src *; script-src *; style-src *; img-src *; frame-src *; connect-src *; font-src *; object-src *; media-src *; frame-ancestors *;" always;
```