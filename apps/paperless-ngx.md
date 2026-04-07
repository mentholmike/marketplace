---
id: paperless-ngx
name: Paperless-Ngx
category: Utilities
description: Document management system. Scan, index, and archive your paper documents with full-text search across all PDFs.
image: ghcr.io/paperless-ngx/paperless-ngx:latest
ports: [8000]
---

# Paperless-Ngx

## Description
Document management system. Scan, index, and archive your paper documents with full-text search across all PDFs.

## Ports
- **8000 — Web interface**

## Docker Compose
```yaml
services:
  paperless-ngx:
    image: ghcr.io/paperless-ngx/paperless-ngx:latest
    container_name: paperless-ngx
    volumes:
      - ./paperless-ngx/data:/data
    ports:
      - "8000:8000"
    restart: unless-stopped
```
