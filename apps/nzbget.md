---
id: nzbget
name: Nzbget
category: Torrents
description: Optimized Usenet downloader. Fast and efficient NZB download client with a lightweight web interface.
image: lscr.io/linuxserver/nzbget:latest
ports: [6789]
---

# Nzbget

## Description
Optimized Usenet downloader. Fast and efficient NZB download client with a lightweight web interface.

## Ports
- **6789 — Web interface**

## Docker Compose
```yaml
services:
  nzbget:
    image: lscr.io/linuxserver/nzbget:latest
    container_name: nzbget
    volumes:
      - ./nzbget/data:/data
    ports:
      - "6789:6789"
    restart: unless-stopped
```
