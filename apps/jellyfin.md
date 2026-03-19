---
id: jellyfin
name: Jellyfin
category: media-servers
description: The free software media system. Stream your media to any device with no fees and no tracking.
image: jellyfin/jellyfin:latest
ports: [8096, 8920]
environment:
  - name: JELLYFIN_PublishedServerUrl
    description: Public server URL for remote access
    required: false
  - name: TZ
    description: Timezone
    required: false
    default: UTC
volumes:
  - name: config
    description: Jellyfin configuration directory
    required: true
    default: ./jellyfin/config
  - name: cache
    description: Cache directory
    required: false
    default: ./jellyfin/cache
  - name: media
    description: Media library mount point
    required: true
    default: ./jellyfin/media
---

# Jellyfin

## Description
Jellyfin is a free software media system that lets you stream your media to any device. No fees, no tracking, full control.

## Ports
- **8096** — Web interface (HTTP)
- **8920** — Web interface (HTTPS)

## Environment Variables
| Variable | Required | Default | Description |
|----------|----------|---------|-------------|
| `JELLYFIN_PublishedServerUrl` | No | — | Public URL for remote access |
| `TZ` | No | UTC | Timezone |

## Volumes
| Volume | Description |
|--------|-------------|
| `config` | Jellyfin configuration and metadata |
| `cache` | Temporary cache files |
| `media` | Your media library |

## Docker Compose
```yaml
services:
  jellyfin:
    image: jellyfin/jellyfin:latest
    container_name: jellyfin
    ports:
      - "8096:8096"
      - "8920:8920"
    environment:
      - JELLYFIN_PublishedServerUrl=${JELLYFIN_PublishedServerUrl}
      - TZ=${TZ:-UTC}
    volumes:
      - ./jellyfin/config:/config
      - ./jellyfin/cache:/cache
      - ./jellyfin/media:/media
    restart: unless-stopped
```

## Notes
- Jellyfin requires FFMEPG for hardware transcoding (add `/dev/video:/dev/video` for hardware acceleration)
- Mount your media to `./jellyfin/media` before starting
- Create accounts and add media library from the web UI
