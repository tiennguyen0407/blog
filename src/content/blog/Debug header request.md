---
author: Tien Nguyen
pubDatetime: 2024-11-26
modDatetime: 2024-11-26
title: How to easy debug request in pod or everywhere want
slug: how-to-easy-debug-request-in-pod-or-everywhere-you-want
featured: true
draft: false
tags:
  - docs
  - debug
  - devops
  - request
  - trick
  - ngrep
  - http
description: How to easy debug request in pod or everywhere want
---
- Use ngrep
```bash
ngrep -W byline -d any port 80
```
