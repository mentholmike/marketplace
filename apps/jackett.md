---
id: jackett
name: Jackett
category: search
description: API support for torrent trackers. Translates queries from Sonarr/Radarr to tracker-specific queries.
image: linuxserver/jackett:latest
ports: [9117]
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
    description: Jackett configuration directory
    required: true
    default: ./jackett/config
  - name: downloads
    description: Downloaded files directory
    required: false
    default: ./jackett/downloads
---

# Jackett

## Description
Jackett provides an API for torrent trackers that Sonarr and Radarr use to search for content. It translates queries into tracker-specific formats.

## Ports
- **9117** — Web interface

## Environment Variables
| Variable | Required | Default | Description |
|----------|----------|---------|-------------|
| `PUID` | No | 1000 | User ID for file permissions |
| `PGID` | No | 1000 | Group ID for file permissions |
| `TZ` | No | UTC | Timezone |

## Volumes
| Volume | Description |
|--------|-------------|
| `config` | Jackett configuration |
| `downloads` | Downloaded files (optional) |

## Docker Compose
```yaml
services:
  jackett:
    image: linuxserver/jackett:latest
    container_name: jackett
    ports:
      - "9117:9117"
    environment:
      - PUID=${PUID:-1000}
      - PGID=${PGID:-1000}
      - TZ=${TZ:-UTC}
    volumes:
      - ./jackett/config:/config
      - ./jackett/downloads:/downloads
    restart: unless-stopped
```

## Notes
- Access Jackett at `http://your-server:9117`
- Add indexers from the web interface (many are pre-configured)
- Copy the Jackett API URL and add it as an indexer in Sonarr/Radarr
- Use the All Providers view to test searches
