---
author: Tien Nguyen
pubDatetime: 2024-11-26
modDatetime: 2024-11-26
title: Fluent Bit push log from WINDOW to Loki
slug: fluent-bit-push-log-from-window-to-loki
featured: true
draft: false
tags:
  - docs
  - logs
  - loki
  - devops
description: Blog
---


- Fluent bit get file log and push to loki
```
[INPUT]
    Name         tail
    Path		 C:\Website\glassfishv3\glassfish\domains\beta\logs\server.log_*

[OUTPUT]
    Name        loki
    Match       *
    Host        54.196.231.71
    Port        3100
    Uri         /loki/api/v1/push
    Labels      job=uat-rails, hostname=uat-rails
```
- Window
```
Restart-Service fluent-bit
get-Service fluent-bit | format-list
```