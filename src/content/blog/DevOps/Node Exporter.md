---
author: Tien Nguyen
pubDatetime: 2024-11-26
modDatetime: 2024-11-26
title: How to install node exporter in linux
slug: how-to-install-node-export-in-linux
featured: true
draft: false
tags:
  - docs
  - prometheus
  - grafana
  - monitor
  - logs
  - node_exporter
  - infra
description: How to install node exporter in linux ( step by step )
---

- Install Binary
```bash
wget https://github.com/prometheus/node_exporter/releases/download/v1.8.2/node_exporter-1.8.2.linux-amd64.tar.gz
```
- Unzip
```
tar -xvf node_exporter-1.8.2.linux-amd64.tar.gz
```
- Copy to bin
```
sudo cp node_exporter-1.8.2.linux-amd64/node_exporter /usr/local/bin
```
- Add user
```
sudo useradd node_exporter --no-create-home --shell /bin/false
```
- Set permission
```
sudo chown node_exporter:node_exporter /usr/local/bin/node_exporter
```
- Create service file
```
sudo vi /etc/system/systemd/node_exporter.service
```
```
[Unit]  
Description=Node Exporter  
Wants=network-online.target  
After=network-online.target  
  
[Service]  
User=node_exporter  
Group=node_exporter  
Type=simple  
ExecStart=/usr/local/bin/node_exporter  
  
[Install]  
WantedBy=multi-user.target
```
- Start service
```
sudo systemctl daemon-reload
sudo systemctl start node_exporter  
sudo systemctl enable node_exporter
sudo systemctl status node_exporter
```