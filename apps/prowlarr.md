---
id: prowlarr
name: Prowlarr
category: arr-stack
description: Indexer manager and proxy for your Arr stack. Manages all your indexers in one place.
image: linuxserver/prowlarr:latest
ports: [9696]
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
volumes:
  - name: config
    description: Prowlarr configuration directory
    required: true
    default: ./prowlarr/config
---

# Prowlarr

## Description
Prowlarr is an indexer manager and proxy for your Arr stack (Sonarr, Radarr, Lidarr). It manages all your Usenet and BitTorrent indexers in one place.

## Ports
- **9696** — Web interface

## Environment Variables
| Variable | Required | Default | Description |
|----------|----------|---------|-------------|
| `PUID` | No | 1000 | User ID for file permissions |
| `PGID` | No | 1000 | Group ID for file permissions |
| `TZ` | No | UTC | Timezone |

## Volumes
| Volume | Description |
|--------|-------------|
| `config` | Prowlarr configuration |

## Docker Compose
```yaml
services:
  prowlarr:
    image: linuxserver/prowlarr:latest
    container_name: prowlarr
    ports:
      - "9696:9696"
    environment:
      - PUID=${PUID:-1000}
      - PGID=${PGID:-1000}
      - TZ=${TZ:-UTC}
    volumes:
      - ./prowlarr/config:/config
    restart: unless-stopped
```

## Notes
- Connect Prowlarr to Sonarr and Radarr as an indexer source
- Add your Usenet and BitTorrent indexers in Prowlarr settings
- Enable indexer sync in your Arr apps to use Prowlarr
