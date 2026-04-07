---
id: bazarr
name: Bazarr
category: Media Servers
description: Subtitle download manager for your Arr stack. Automatically finds and downloads subtitles for movies and TV shows.
image: lscr.io/linuxserver/bazarr:latest
ports: [6767]
---

# Bazarr

## Description
Subtitle download manager for your Arr stack. Automatically finds and downloads subtitles for movies and TV shows.

## Ports
- **6767 — Web interface**

## Docker Compose
```yaml
services:
  bazarr:
    image: lscr.io/linuxserver/bazarr:latest
    container_name: bazarr
    volumes:
      - ./bazarr/data:/data
    ports:
      - "6767:6767"
    restart: unless-stopped
```
