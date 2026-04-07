---
id: bookstack
name: Bookstack
category: Productivity
description: Platform for storing and organizing information. Create a wiki, documentation, or knowledge base with a clean book-and-page structure.
image: lscr.io/linuxserver/bookstack:latest
ports: [6875]
---

# Bookstack

## Description
Platform for storing and organizing information. Create a wiki, documentation, or knowledge base with a clean book-and-page structure.

## Ports
- **6875 — Web interface**

## Docker Compose
```yaml
services:
  bookstack:
    image: lscr.io/linuxserver/bookstack:latest
    container_name: bookstack
    volumes:
      - ./bookstack/data:/data
    ports:
      - "6875:6875"
    restart: unless-stopped
```
