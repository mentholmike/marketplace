---
id: qbittorrent
name: qBittorrent
category: torrents
description: Free and open-source BitTorrent client. Feature-rich alternative to Transmission with a modern web UI.
image: linuxserver/qbittorrent:latest
ports: [8080, 6881]
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
    description: qBittorrent configuration directory
    required: true
    default: ./qbittorrent/config
  - name: downloads
    description: Downloaded files directory
    required: true
    default: ./qbittorrent/downloads
---

# qBittorrent

## Description
qBittorrent is a free and open-source BitTorrent client with a modern web UI. More feature-rich than Transmission with built-in search and sequential downloading.

## Ports
- **8080** — Web interface
- **6881** — BitTorrent peer connections (TCP)

## Environment Variables
| Variable | Required | Default | Description |
|----------|----------|---------|-------------|
| `PUID` | No | 1000 | User ID for file permissions |
| `PGID` | No | 1000 | Group ID for file permissions |
| `TZ` | No | UTC | Timezone |

## Volumes
| Volume | Description |
|--------|-------------|
| `config` | qBittorrent configuration |
| `downloads` | Downloaded files |

## Docker Compose
```yaml
services:
  qbittorrent:
    image: linuxserver/qbittorrent:latest
    container_name: qbittorrent
    ports:
      - "8080:8080"
      - "6881:6881/tcp"
    environment:
      - PUID=${PUID:-1000}
      - PGID=${PGID:-1000}
      - TZ=${TZ:-UTC}
    volumes:
      - ./qbittorrent/config:/config
      - ./qbittorrent/downloads:/downloads
    restart: unless-stopped
```

## Notes
- Access qBittorrent at `http://your-server:8080`
- Default login: admin / adminadmin
- Configure port forwarding on 6881 for better peer connections
- The web UI runs on port 8080 inside the container
