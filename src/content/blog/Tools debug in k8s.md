---
author: Tien Nguyen
pubDatetime: 2024-11-26
modDatetime: 2024-11-26
title: Tools debug in k8s
slug: tools-debug-in-k8s
featured: true
draft: false
tags:
  - docs
  - k8s
  - debug
  - devops
  - trick
description: Tools debug in k8s
---
- Debug network
```bash
```
- Debug mongo
```bash
kubectl run mongodb-client \
	--image=tiennguyen47/backup-mongodb:main-3d901a68-1719911260 \
	--restart=Never \
	-- sh -c "while true; do echo 'debug' && sleep 5; done;"
```
- Debug postgres
```bash
kubectl run postgres-client \
	--image=tiennguyen47/backup-postgres:main-9b0f06af-1696695606 \
	--restart=Never
```
- Debug
```bash
kubectl run debug \
	--image=tiennguyen47/alpine-tools:latest \
	--restart=Never -- sh -c "while true; do echo 'debug' && sleep 5; done;"
```
- Stress test ( DDOS )
```bash
kubectl run spam-without-proxy \
	--image=tiennguyen47/spam:latest \
	--restart=Never \
	--env="TARGET_HOST=https://xxx.yyy" \
	--env="NUMBER_REQUESTS=300" \
	--env="CONCURRENT_REQUESTS=100" \
	--env="TIMEOUT=15s" \
	--env="METHOD=GET" \
	--env="INFINITY=true"
```