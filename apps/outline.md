---
id: outline
name: Outline
category: Productivity
description: Fast, collaborative wiki for teams. Beautiful documentation that makes it easy to share knowledge.
image: docker.getoutline.com/outline/wiki:latest
ports: [3000]
---

# Outline

## Description
Fast, collaborative wiki for teams. Beautiful documentation that makes it easy to share knowledge.

## Ports
- **3000 — Web interface**

## Docker Compose
```yaml
services:
  outline:
    image: docker.getoutline.com/outline/wiki:latest
    container_name: outline
    volumes:
      - ./outline/data:/data
    ports:
      - "3000:3000"
    restart: unless-stopped
```
