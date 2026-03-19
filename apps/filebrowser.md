---
id: filebrowser
name: Filebrowser
category: cloud-storage
description: Self-hosted file manager with a web interface. Upload, download, and manage files on your server through a clean UI.
image: filebrowser/filebrowser:latest
ports: [8080]
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
  - name: filebrowser-data
    description: Filebrowser database and settings
    required: true
    default: ./filebrowser/data
  - name: filebrowser-root
    description: Root directory to manage
    required: true
    default: ./filebrowser/root
---

# Filebrowser

## Description
Filebrowser provides a file manager web interface for your server. Upload, download, delete, rename, and organize files through a clean browser-based UI. Perfect for managing server files without SSH.

## Ports
- **8080** — Web interface

## Environment Variables
| Variable | Required | Default | Description |
|----------|----------|---------|-------------|
| `PUID` | No | 1000 | User ID for file permissions |
| `PGID` | No | 1000 | Group ID for file permissions |
| `TZ` | No | UTC | Timezone |

## Volumes
| Volume | Description |
|--------|-------------|
| `filebrowser-data` | Filebrowser database and settings |
| `filebrowser-root` | Root directory to manage |

## Docker Compose
```yaml
services:
  filebrowser:
    image: filebrowser/filebrowser:latest
    container_name: filebrowser
    ports:
      - "8080:8080"
    environment:
      - PUID=${PUID:-1000}
      - PGID=${PGID:-1000}
      - TZ=${TZ:-UTC}
    volumes:
      - ./filebrowser/data:/data
      - ./filebrowser/root:/srv
    restart: unless-stopped
```

## Notes
- Access Filebrowser at `http://your-server:8080`
- Default login: admin / admin
- Change the admin password on first login
- Mount any directory on your server to `./filebrowser/root` to manage it
- Create additional users with different directory permissions
- Enable sharing links for easy file sharing without account creation
