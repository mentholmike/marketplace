---
id: portainer
name: Portainer
category: Container Management
description: Docker container management UI. Manage containers, images, volumes, and networks through a clean web interface.
image: portainer/portainer-ce:alpine
ports: [9000,9443]
---

# Portainer

## Description
Docker container management UI. Manage containers, images, volumes, and networks through a clean web interface.

## Ports
- **9000 — HTTP, 9443 — HTTPS**

## Docker Compose
```yaml
services:
  portainer:
    image: portainer/portainer-ce:alpine
    container_name: portainer
    volumes:
      - ./portainer/data:/data
    ports:
      - "9000:9000"
    restart: unless-stopped
```
