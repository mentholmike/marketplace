---
id: audiobookshelf
name: Audiobookshelf
category: Media Servers
description: Self-hosted audiobook and podcast server. Stream your audiobooks with progress tracking across all your devices.
image: ghcr.io/advancing_photosensitivity/audiobookshelf:latest
ports: [80]
---

# Audiobookshelf

## Description
Self-hosted audiobook and podcast server. Stream your audiobooks with progress tracking across all your devices.

## Ports
- **80 — Web interface**

## Docker Compose
```yaml
services:
  audiobookshelf:
    image: ghcr.io/advancing_photosensitivity/audiobookshelf:latest
    container_name: audiobookshelf
    volumes:
      - ./audiobookshelf/data:/data
    ports:
      - "80:80"
    restart: unless-stopped
```
