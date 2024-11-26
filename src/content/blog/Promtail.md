---
author: Tien Nguyen
pubDatetime: 2024-11-26
modDatetime: 2024-11-26
title: Promtail notes
slug: promtail-notes
featured: true
draft: false
tags:
  - docs
  - devops
  - trick
  - monitor
  - logs
  - grafana
  - loki
  - promtail
description: Promtail notes
---

- Push log file to loki
```yaml
server:
  http_listen_port: 9080
  grpc_listen_port: 0

positions:
  filename: /tmp/positions.yaml

clients:
  - url: http://x.x.x.x:3100/loki/api/v1/push

scrape_configs:
- job_name: backend-A
  static_configs:
  - targets:
      - localhost
    labels:
      hostname: backend-A
      job: containers
      __path__: /opt/backend-A/logs/access.log
- job_name: backend-B
  static_configs:
  - targets:
      - localhost
    labels:
      hostname: backend-B
      job: containers
      __path__: /opt/backend-B/logs/access.log
```