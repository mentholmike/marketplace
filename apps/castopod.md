---
id: castopod
name: Castopod
category: Media Servers
description: Self-hosted podcast hosting platform. Publish, distribute, and monetize your podcast with built-in analytics.
image: castopodapp/castopod:latest
ports: [8000]
---

# Castopod

## Description
Self-hosted podcast hosting platform. Publish, distribute, and monetize your podcast with built-in analytics.

## Ports
- **8000 — Web interface**

## Docker Compose
```yaml
services:
  castopod:
    image: castopodapp/castopod:latest
    container_name: castopod
    volumes:
      - ./castopod/data:/data
    ports:
      - "8000:8000"
    restart: unless-stopped
```
