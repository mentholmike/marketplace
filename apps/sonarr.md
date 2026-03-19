---
id: sonarr
name: Sonarr
category: arr-stack
description: Smart PVR for newsgroup and bittorrent users. Automatically downloads TV shows via Usenet or BitTorrent.
image: linuxserver/sonarr:latest
ports: [8989]
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
    description: Sonarr configuration directory
    required: true
    default: ./sonarr/config
  - name: tv
    description: TV shows directory
    required: true
    default: ./sonarr/tv
  - name: downloads
    description: Downloaded files directory
    required: true
    default: ./sonarr/downloads
---

# Sonarr

## Description
Sonarr (formerly NzbDrone) is a PVR for Usenet and BitTorrent users. It monitors RSS feeds for new episodes and automatically downloads them.

## Ports
- **8989** — Web interface

## Environment Variables
| Variable | Required | Default | Description |
|----------|----------|---------|-------------|
| `PUID` | No | 1000 | User ID for file permissions |
| `PGID` | No | 1000 | Group ID for file permissions |
| `TZ` | No | UTC | Timezone |

## Volumes
| Volume | Description |
|--------|-------------|
| `config` | Sonarr configuration |
| `tv` | TV shows library |
| `downloads` | Downloaded episodes |

## Docker Compose
```yaml
services:
  sonarr:
    image: linuxserver/sonarr:latest
    container_name: sonarr
    ports:
      - "8989:8989"
    environment:
      - PUID=${PUID:-1000}
      - PGID=${PGID:-1000}
      - TZ=${TZ:-UTC}
    volumes:
      - ./sonarr/config:/config
      - ./sonarr/tv:/tv
      - ./sonarr/downloads:/downloads
    restart: unless-stopped
```

## Notes
- Connect Sonarr to your download client (Sabnzbd, Transmission, qBittorrent, etc.)
- Add your indexer in Sonarr settings
- Point to your TV show folder in the library setup
