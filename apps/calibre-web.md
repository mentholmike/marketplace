---
id: calibre-web
name: Calibre-Web
category: Cloud Storage
description: Modern web UI for Calibre e-book server. Access and read your ebook library from any device.
image: lscr.io/linuxserver/calibre-web:latest
ports: [8083]
---

# Calibre-Web

## Description
Modern web UI for Calibre e-book server. Access and read your ebook library from any device.

## Ports
- **8083 — Web interface**

## Docker Compose
```yaml
services:
  calibre-web:
    image: lscr.io/linuxserver/calibre-web:latest
    container_name: calibre-web
    volumes:
      - ./calibre-web/data:/data
    ports:
      - "8083:8083"
    restart: unless-stopped
```
