---
id: homarr
name: Homarr
category: Utilities
description: Sleek homepage dashboard for your server. Organize your services, monitor status, and access everything from one place.
image: ghcr.io/ajnart/homarr:latest
ports: [7575]
---

# Homarr

## Description
Sleek homepage dashboard for your server. Organize your services, monitor status, and access everything from one place.

## Ports
- **7575 — Web interface**

## Docker Compose
```yaml
services:
  homarr:
    image: ghcr.io/ajnart/homarr:latest
    container_name: homarr
    volumes:
      - ./homarr/data:/data
    ports:
      - "7575:7575"
    restart: unless-stopped
```
