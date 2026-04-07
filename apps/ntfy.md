---
id: ntfy
name: Ntfy
category: Notifications
description: Send push notifications to your phone or desktop from anywhere. Self-hosted notify-at-the-command-line service.
image: binwiederhier/ntfy:latest
ports: [80]
---

# Ntfy

## Description
Send push notifications to your phone or desktop from anywhere. Self-hosted notify-at-the-command-line service.

## Ports
- **80 — Web interface and API**

## Docker Compose
```yaml
services:
  ntfy:
    image: binwiederhier/ntfy:latest
    container_name: ntfy
    volumes:
      - ./ntfy/data:/data
    ports:
      - "80:80"
    restart: unless-stopped
```
