---
id: watchtower
name: Watchtower
category: Container Management
description: Automatic container updates. Monitors your Docker containers and automatically updates them when new images are available.
image: containrrr/watchtower:latest
ports: []
---

# Watchtower

## Description
Automatic container updates. Monitors your Docker containers and automatically updates them when new images are available.

## Ports
- **No ports — runs in background**

## Docker Compose
```yaml
services:
  watchtower:
    image: containrrr/watchtower:latest
    container_name: watchtower
    volumes:
      - ./watchtower/data:/data

    restart: unless-stopped
```
