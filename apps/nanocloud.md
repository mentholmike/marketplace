---
id: nanocloud
name: NanoCloud
category: cloud-storage
description: Self-hosted file sharing and collaboration. Share files with anyone via links, no account required.
image: nanocloud/nanocloud:latest
ports: [4000]
environment:
  - name: ADMIN_EMAIL
    description: Admin email address
    required: false
  - name: ADMIN_PASSWORD
    description: Admin password
    required: false
  - name: NEXTAUTH_SECRET
    description: NextAuth secret key
    required: false
  - name: DATABASE_URL
    description: SQLite database path
    required: false
    default: /data/nanocloud.db
  - name: TZ
    description: Timezone
    required: false
    default: UTC
volumes:
  - name: nanocloud-data
    description: NanoCloud data directory
    required: true
    default: ./nanocloud/data
  - name: nanocloud-files
    description: Shared files storage
    required: true
    default: ./nanocloud/files
---

# NanoCloud

## Description
NanoCloud is a minimal, self-hosted file sharing platform. Upload files and share them with anyone through a simple link. No account required for recipients — just upload and share.

## Ports
- **4000** — Web interface

## Environment Variables
| Variable | Required | Default | Description |
|----------|----------|---------|-------------|
| `ADMIN_EMAIL` | No | — | Admin email address |
| `ADMIN_PASSWORD` | No | — | Admin password |
| `NEXTAUTH_SECRET` | No | — | NextAuth secret key |
| `DATABASE_URL` | No | /data/nanocloud.db | SQLite database path |
| `TZ` | No | UTC | Timezone |

## Volumes
| Volume | Description |
|--------|-------------|
| `nanocloud-data` | NanoCloud data and database |
| `nanocloud-files` | Shared files storage |

## Docker Compose
```yaml
services:
  nanocloud:
    image: nanocloud/nanocloud:latest
    container_name: nanocloud
    ports:
      - "4000:4000"
    environment:
      - ADMIN_EMAIL=${ADMIN_EMAIL}
      - ADMIN_PASSWORD=${ADMIN_PASSWORD}
      - NEXTAUTH_SECRET=${NEXTAUTH_SECRET}
      - DATABASE_URL=${DATABASE_URL:-/data/nanocloud.db}
      - TZ=${TZ:-UTC}
    volumes:
      - ./nanocloud/data:/data
      - ./nanocloud/files:/files
    restart: unless-stopped
```

## Notes
- Access NanoCloud at `http://your-server:4000`
- Create an admin account on first run
- Upload files and share via link — recipients don't need an account
- Set expiration dates and download limits on shared links
- Optional password protection for sensitive files
- Clean, minimal interface focused on simplicity
