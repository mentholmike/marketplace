---
id: traefik
name: Traefik
category: Networking
description: Modern reverse proxy and load balancer. Automatically routes traffic to your containers with automatic SSL via Let's Encrypt.
image: traefik:v3.0
ports: [80,443,8080]
---

# Traefik

## Description
Modern reverse proxy and load balancer. Automatically routes traffic to your containers with automatic SSL via Let's Encrypt.

## Ports
- **80 — HTTP, 443 — HTTPS, 8080 — Dashboard**

## Docker Compose
```yaml
services:
  traefik:
    image: traefik:v3.0
    container_name: traefik
    volumes:
      - ./traefik/data:/data
    ports:
      - "80:80"
    restart: unless-stopped
```
