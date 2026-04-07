---
id: adguard-home
name: Adguard-Home
category: Networking
description: Network-wide DNS-level ad blocking and parental controls. Blocks ads and trackers across your entire network.
image: adguard/adguardhome:latest
ports: [53,853,3000]
---

# Adguard-Home

## Description
Network-wide DNS-level ad blocking and parental controls. Blocks ads and trackers across your entire network.

## Ports
- **53 — DNS (TCP/UDP), 853 — DoT, 3000 — Web interface**

## Docker Compose
```yaml
services:
  adguard-home:
    image: adguard/adguardhome:latest
    container_name: adguard-home
    volumes:
      - ./adguard-home/data:/data
    ports:
      - "53:53"
    restart: unless-stopped
```
