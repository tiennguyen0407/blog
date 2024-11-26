---
author: Tien Nguyen
pubDatetime: 2024-11-26
modDatetime: 2024-11-26
title: Git notes
slug: git-notes
featured: true
draft: false
tags:
  - docs
  - git
  - trick
  - devops
description: Git notes
---

- Fix key for repo private
```bash
git config --global url."https://devops:${PULL_LIB}@gitlab.xxx.yyy/".insteadOf "https://gitlab.xxx.yyy/"
```