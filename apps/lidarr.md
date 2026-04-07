---
id: lidarr
name: Lidarr
category: Media Servers
description: Usenet and BitTorrent music collection manager. Automatically downloads and organizes your music.
image: lscr.io/linuxserver/lidarr:latest
ports: [8686]
---

# Lidarr

## Description
Usenet and BitTorrent music collection manager. Automatically downloads and organizes your music.

## Ports
- **8686 — Web interface**

## Docker Compose
```yaml
services:
  lidarr:
    image: lscr.io/linuxserver/lidarr:latest
    container_name: lidarr
    volumes:
      - ./lidarr/data:/data
    ports:
      - "8686:8686"
    restart: unless-stopped
```
