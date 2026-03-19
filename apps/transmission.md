---
id: transmission
name: Transmission
category: torrents
description: Lightweight BitTorrent client. Simple, efficient, and cross-platform torrent downloading.
image: linuxserver/transmission:latest
ports: [9091, 51413]
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
    description: Transmission configuration directory
    required: true
    default: ./transmission/config
  - name: downloads
    description: Downloaded files directory
    required: true
    default: ./transmission/downloads
  - name: watch
    description: Watch folder for auto-add torrents
    required: false
    default: ./transmission/watch
---

# Transmission

## Description
Transmission is a lightweight BitTorrent client known for its simplicity and efficiency. Features a web UI for remote management.

## Ports
- **9091** — Web interface
- **51413** — BitTorrent peer connections (TCP/UDP)

## Environment Variables
| Variable | Required | Default | Description |
|----------|----------|---------|-------------|
| `PUID` | No | 1000 | User ID for file permissions |
| `PGID` | No | 1000 | Group ID for file permissions |
| `TZ` | No | UTC | Timezone |

## Volumes
| Volume | Description |
|--------|-------------|
| `config` | Transmission configuration |
| `downloads` | Downloaded files |
| `watch` | Watch folder for auto-add torrents (optional) |

## Docker Compose
```yaml
services:
  transmission:
    image: linuxserver/transmission:latest
    container_name: transmission
    ports:
      - "9091:9091"
      - "51413:51413"
      - "51413:51413/udp"
    environment:
      - PUID=${PUID:-1000}
      - PGID=${PGID:-1000}
      - TZ=${TZ:-UTC}
    volumes:
      - ./transmission/config:/config
      - ./transmission/downloads:/downloads
      - ./transmission/watch:/watch
    restart: unless-stopped
```

## Notes
- Access Transmission at `http://your-server:9091`
- Default login: admin / admin
- Mount a watch folder to `./transmission/watch` for automatic torrent adding
- Configure port forwarding on 51413 for better peer connections
