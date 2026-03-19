---
id: plex
name: Plex Media Server
category: media-servers
description: Stream your media anywhere. Organize and stream your movies, TV shows, music, and photos to any device.
image: plexinc/pms-docker:latest
ports: [32400]
environment:
  - name: PLEX_CLAIM
    description: Plex claim token (get from plex.tv/claim)
    required: false
  - name: TZ
    description: Timezone
    required: false
    default: UTC
volumes:
  - name: config
    description: Plex configuration directory
    required: true
    default: ./plex/config
  - name: media
    description: Media library mount point
    required: true
    default: ./plex/media
  - name: transcodes
    description: Temporary transcoding directory
    required: false
    default: ./plex/transcodes
---

# Plex Media Server

## Description
Plex Media Server organizes your media library and streams it to any device. Get your claim token from [plex.tv/claim](https://www.plex.tv/claim).

## Ports
- **32400** — Web interface and streaming

## Environment Variables
| Variable | Required | Default | Description |
|----------|----------|---------|-------------|
| `PLEX_CLAIM` | No | — | Plex claim token from plex.tv/claim |
| `TZ` | No | UTC | Timezone |

## Volumes
| Volume | Description |
|--------|-------------|
| `config` | Plex configuration and metadata |
| `media` | Your media library |
| `transcodes` | Temporary transcoding files (optional) |

## Docker Compose
```yaml
services:
  plex:
    image: plexinc/pms-docker:latest
    container_name: plex
    network_mode: host
    environment:
      - PLEX_CLAIM=${PLEX_CLAIM}
      - TZ=${TZ:-UTC}
      - ADVERTISE_IP=http://YOUR_SERVER_IP:32400
    volumes:
      - ./plex/config:/config
      - ./plex/media:/data
      - ./plex/transcodes:/transcode
    restart: unless-stopped
```

## Notes
- Replace `YOUR_SERVER_IP` with your server's local IP address
- Mount your media to `./plex/media` before starting
- For remote access, configure Plex to use your domain in settings
