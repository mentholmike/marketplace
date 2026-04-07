---
id: komga
name: Komga
category: Media Servers
description: Media server for comics and ebooks. Browse, read, and organize your comic (CBZ/CBR) and ebook (EPUB) library.
image: gotson/komga:latest
ports: [25600]
---

# Komga

## Description
Media server for comics and ebooks. Browse, read, and organize your comic (CBZ/CBR) and ebook (EPUB) library.

## Ports
- **25600 — Web interface**

## Docker Compose
```yaml
services:
  komga:
    image: gotson/komga:latest
    container_name: komga
    volumes:
      - ./komga/data:/data
    ports:
      - "25600:25600"
    restart: unless-stopped
```
