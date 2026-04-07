---
id: freshrss
name: Freshrss
category: Notifications
description: Self-hosted RSS/Atom feed reader. Subscribe to feeds and read them in a clean, customizable interface.
image: freshrss/freshrss:latest
ports: [8080]
---

# Freshrss

## Description
Self-hosted RSS/Atom feed reader. Subscribe to feeds and read them in a clean, customizable interface.

## Ports
- **8080 — Web interface**

## Docker Compose
```yaml
services:
  freshrss:
    image: freshrss/freshrss:latest
    container_name: freshrss
    volumes:
      - ./freshrss/data:/data
    ports:
      - "8080:8080"
    restart: unless-stopped
```
