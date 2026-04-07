---
id: umami
name: Umami
category: Analytics
description: Simple, fast, privacy-focused web analytics. Track page views and visitor behavior without using Google Analytics.
image: ghcr.io/umami-software/umami:postgresql-latest
ports: [3000]
---

# Umami

## Description
Simple, fast, privacy-focused web analytics. Track page views and visitor behavior without using Google Analytics.

## Ports
- **3000 — Web interface**

## Docker Compose
```yaml
services:
  umami:
    image: ghcr.io/umami-software/umami:postgresql-latest
    container_name: umami
    volumes:
      - ./umami/data:/data
    ports:
      - "3000:3000"
    restart: unless-stopped
```
