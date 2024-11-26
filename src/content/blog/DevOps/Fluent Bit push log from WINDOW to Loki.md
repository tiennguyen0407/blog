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
  - monitor
  - fluent-bit
  - fluent
description: Fluent Bit push log from WINDOW to Loki
---


- Fluent bit get file log and push to loki
```json
[INPUT]
    Name         tail
    Path		 C:\Website\abc\logs\server.log_*

[OUTPUT]
    Name        loki
    Match       *
    Host        x.x.x.x
    Port        3100
    Uri         /loki/api/v1/push
    Labels      job=backend-A, hostname=backend-A
```
- Window
```powershell
Restart-Service fluent-bit
get-Service fluent-bit | format-list
```