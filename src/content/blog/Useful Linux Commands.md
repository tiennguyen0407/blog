---
author: Tien Nguyen
pubDatetime: 2024-11-26
modDatetime: 2024-11-26
title: Useful Linux Commands
slug: useful-linux-commands
featured: true
draft: false
tags:
  - docs
  - bash
  - trick
  - debug
  - devops
description: Discover a selection of essential Linux commands that can boost your productivity and streamline your workflow.
---

- Switch version in linux
```bash
sudo alternatives --config java

EX:
verison 17 => /usr/lib/jvm/java-17-amazon-corretto.aarch64/bin/java
verison 11 => /usr/lib/jvm/java-11-amazon-corretto.aarch64/bin/java
```
- Count file in folder and sub folder
```bash
find . -maxdepth 1 -type d | while read -r dir do printf "%s:\t" "$dir"; find "$dir" -type f | wc -l; done
```
- Find file with content
```bash
grep -rnw '/path/to/somewhere/' -e 'pattern'
```
- Find large file
```bash
find . -type f -size +100M
```