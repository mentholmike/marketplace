---
id: readarr
name: Readarr
category: Media Servers
description: Usenet and BitTorrent ebook collection manager. Automatically downloads and organizes your ebooks.
image: lscr.io/linuxserver/readarr:latest
ports: [8787]
---

# Readarr

## Description
Usenet and BitTorrent ebook collection manager. Automatically downloads and organizes your ebooks.

## Ports
- **8787 — Web interface**

## Docker Compose
```yaml
services:
  readarr:
    image: lscr.io/linuxserver/readarr:latest
    container_name: readarr
    volumes:
      - ./readarr/data:/data
    ports:
      - "8787:8787"
    restart: unless-stopped
```
