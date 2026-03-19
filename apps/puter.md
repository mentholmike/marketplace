---
id: puter
name: Puter
category: cloud-storage
description: Self-hosted cloud operating system. A full desktop environment in your browser with files, apps, and more.
image: https://github.com/Hayao0819/puter-docker
ports: [4000]
environment:
  - name: PUTER_PORT
    description: Port for Puter to listen on
    required: false
    default: "4000"
  - name: TZ
    description: Timezone
    required: false
    default: UTC
volumes:
  - name: puter-data
    description: Puter data directory
    required: true
    default: ./puter/data
---

# Puter

## Description
Puter is a self-hosted cloud operating system that runs in your browser. It provides a full desktop environment with a file manager, code editor, image viewer, terminal, and more — all accessible from any device.

## Ports
- **4000** — Web interface

## Environment Variables
| Variable | Required | Default | Description |
|----------|----------|---------|-------------|
| `PUTER_PORT` | No | 4000 | Port for Puter to listen on |
| `TZ` | No | UTC | Timezone |

## Volumes
| Volume | Description |
|--------|-------------|
| `puter-data` | Puter data directory |

## Docker Compose
```yaml
services:
  puter:
    image: hayoo/puter:latest
    container_name: puter
    ports:
      - "4000:4000"
    environment:
      - PUTER_PORT=${PUTER_PORT:-4000}
      - TZ=${TZ:-UTC}
    volumes:
      - ./puter/data:/app/data
    restart: unless-stopped
```

## Notes
- Access Puter at `http://your-server:4000`
- Use the built-in code editor, terminal, and file manager
- Store files in your own cloud storage
- Multiple users can access the same Puter instance
- Great for accessing your server's files from any browser
