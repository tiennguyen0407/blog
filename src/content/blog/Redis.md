---
author: Tien Nguyen
pubDatetime: 2024-11-25
modDatetime: 2024-11-25
title: Redis notes
slug: redis-note
featured: true
draft: false
tags:
  - docs
  - devops
  - redis
  - trick
description: Redis notes
---

#### Scan key redis in single db
- 1 line
```bash
redis-cli --scan | xargs -I {} sh -c 'usage=$(redis-cli memory usage "{}"); if [ "$usage" != "" ]; then echo "{} $usage"; fi' | awk '{if ($NF/1024/1024 > 0.1) print $1 " => " $NF/1024/1024 " MB"}' | sort -k3 -nr
```
- Multi line
```bash
redis-cli --scan | xargs -I {} sh -c '
    usage=$(redis-cli memory usage "{}")
    if [ "$usage" != "" ]; then
        echo "{} $usage"
    fi
' | awk '
    {
        if ($NF/1024/1024 > 0.1) 
            print $1 " => " $NF/1024/1024 " MB"
    }
' | sort -k3 -nr
```

#### Scan key redis in all db
- 1 line
```bash
for db in $(seq 0 15); do redis-cli -n $db --scan | xargs -I {} sh -c 'usage=$(redis-cli -n '"$db"' memory usage "{}"); if [ "$usage" != "" ]; then echo "{} $usage"; fi' ; done | awk '{if ($NF/1024/1024 > 0.1) print $1 " => " $NF/1024/1024 " MB"}' | sort -k3 -nr
```
- Multi line
```bash
for db in $(seq 0 15); do
    redis-cli -n $db --scan | xargs -I {} sh -c '
        usage=$(redis-cli -n '"$db"' memory usage "{}")
        if [ "$usage" != "" ]; then
            echo "{} $usage"
        fi
    '
done | awk '{if ($NF/1024/1024 > 0.1) print $1 " => " $NF/1024/1024 " MB"}' | sort -k3 -nr
```

#### Create new file AOF ( decrease size file AOF )
```
BGREWRITEAOF
```