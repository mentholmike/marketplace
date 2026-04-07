---
id: syncthing
name: Syncthing
category: Utilities
description: Decentralized file synchronization. Keep files in sync between devices without storing data on a third-party server.
image: syncthing/syncthing:latest
ports: [8384]
---

# Syncthing

## Description
Decentralized file synchronization. Keep files in sync between devices without storing data on a third-party server.

## Ports
- **8384 — Web interface**

## Docker Compose
```yaml
services:
  syncthing:
    image: syncthing/syncthing:latest
    container_name: syncthing
    volumes:
      - ./syncthing/data:/data
    ports:
      - "8384:8384"
    restart: unless-stopped
```
