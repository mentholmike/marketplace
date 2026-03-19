---
id: rsshub
name: RSSHub
category: utilities
description: Open source RSS feed generator. Generate RSS feeds from websites that don't have them.
image: diygod/rsshub:latest
ports: [1200]
environment:
  - name: PUID
    description: User ID for file permissions
    required: false
    default: "1000"
  - name: PGID
    description: Group ID for file permissions
    required: false
    default: "1000"
  - name: TZ
    description: Timezone
    required: false
    default: UTC
  - name: PORT
    description: Internal port
    required: false
    default: "1200"
volumes:
  - name: rsshub-data
    description: RSSHub data directory
    required: true
    default: ./rsshub/data
---

# RSSHub

## Description
RSSHub is an open source RSS feed generator. It can generate RSS feeds from almost any website, making it easy to follow content from sites that don't natively support RSS.

## Ports
- **1200** — Web interface and API

## Environment Variables
| Variable | Required | Default | Description |
|----------|----------|---------|-------------|
| `PUID` | No | 1000 | User ID for file permissions |
| `PGID` | No | 1000 | Group ID for file permissions |
| `TZ` | No | UTC | Timezone |
| `PORT` | No | 1200 | Internal port |

## Volumes
| Volume | Description |
|--------|-------------|
| `rsshub-data` | RSSHub data directory |

## Docker Compose
```yaml
services:
  rsshub:
    image: diygod/rsshub:latest
    container_name: rsshub
    ports:
      - "1200:1200"
    environment:
      - PUID=${PUID:-1000}
      - PGID=${PGID:-1000}
      - TZ=${TZ:-UTC}
      - PORT=${PORT:-1200}
    volumes:
      - ./rsshub/data:/app/data
    restart: unless-stopped
```

## Notes
- Access RSSHub at `http://your-server:1200`
- Visit the homepage to discover available routes
- Generate feed URLs using: `http://your-server:1200/{route}`
- Example: `http://your-server:1200/twitter/user/DownloadRecipes` for Twitter
- Supports hundreds of websites — check `/routes` for all available routes
- For private routes, configure `REDIS_URL` and `GITHUB_ACCESS_TOKEN`
