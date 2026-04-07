---
id: shlink
name: Shlink
category: Utilities
description: Self-hosted URL shortener with statistics and tracking. Create branded short links and track clicks.
image: shlinkio/shlink:stable
ports: [8080]
---

# Shlink

## Description
Self-hosted URL shortener with statistics and tracking. Create branded short links and track clicks.

## Ports
- **8080 — Web interface**

## Docker Compose
```yaml
services:
  shlink:
    image: shlinkio/shlink:stable
    container_name: shlink
    volumes:
      - ./shlink/data:/data
    ports:
      - "8080:8080"
    restart: unless-stopped
```
