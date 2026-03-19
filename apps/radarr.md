---
id: radarr
name: Radarr
category: arr-stack
description: Movie collection manager for Usenet and BitTorrent users. Automatically finds and downloads movies.
image: linuxserver/radarr:latest
ports: [7878]
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
    description: Radarr configuration directory
    required: true
    default: ./radarr/config
  - name: movies
    description: Movies directory
    required: true
    default: ./radarr/movies
  - name: downloads
    description: Downloaded files directory
    required: true
    default: ./radarr/downloads
---

# Radarr

## Description
Radarr is a movie collection manager for Usenet and BitTorrent users. It monitors RSS feeds for new movies and automatically downloads them.

## Ports
- **7878** — Web interface

## Environment Variables
| Variable | Required | Default | Description |
|----------|----------|---------|-------------|
| `PUID` | No | 1000 | User ID for file permissions |
| `PGID` | No | 1000 | Group ID for file permissions |
| `TZ` | No | UTC | Timezone |

## Volumes
| Volume | Description |
|--------|-------------|
| `config` | Radarr configuration |
| `movies` | Movies library |
| `downloads` | Downloaded movies |

## Docker Compose
```yaml
services:
  radarr:
    image: linuxserver/radarr:latest
    container_name: radarr
    ports:
      - "7878:7878"
    environment:
      - PUID=${PUID:-1000}
      - PGID=${PGID:-1000}
      - TZ=${TZ:-UTC}
    volumes:
      - ./radarr/config:/config
      - ./radarr/movies:/movies
      - ./radarr/downloads:/downloads
    restart: unless-stopped
```

## Notes
- Connect Radarr to your download client
- Add your indexer in Radarr settings
- Point to your movies folder in the library setup
