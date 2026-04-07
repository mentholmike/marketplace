---
id: outline-wiki
name: Outline-Wiki
category: Productivity
description: Fast, collaborative wiki for teams. Beautiful documentation with real-time editing and powerful search.
image: docker.getoutline.com/outline/wiki:latest
ports: [3000]
---

# Outline-Wiki

## Description
Fast, collaborative wiki for teams. Beautiful documentation with real-time editing and powerful search.

## Ports
- **3000 — Web interface**

## Docker Compose
```yaml
services:
  outline-wiki:
    image: docker.getoutline.com/outline/wiki:latest
    container_name: outline-wiki
    volumes:
      - ./outline-wiki/data:/data
    ports:
      - "3000:3000"
    restart: unless-stopped
```
