---
id: nextcloud
name: Nextcloud
category: cloud-storage
description: Self-hosted productivity platform. File sync, share, calendar, contacts, tasks, and more — all under your control.
image: nextcloud:latest
ports: [8080]
environment:
  - name: MYSQL_HOST
    description: MySQL database host
    required: true
  - name: MYSQL_DATABASE
    description: MySQL database name
    required: true
  - name: MYSQL_USER
    description: MySQL database user
    required: true
  - name: MYSQL_PASSWORD
    description: MySQL database password
    required: true
  - name: TZ
    description: Timezone
    required: false
    default: UTC
volumes:
  - name: nextcloud-data
    description: Nextcloud data directory
    required: true
    default: ./nextcloud/data
  - name: nextcloud-apps
    description: Nextcloud apps
    required: true
    default: ./nextcloud/apps
  - name: nextcloud-config
    description: Nextcloud configuration
    required: true
    default: ./nextcloud/config
---

# Nextcloud

## Description
Nextcloud is a self-hosted productivity platform. Sync files, share calendars, manage contacts, collaborate on documents, and more — all with full privacy control.

## Ports
- **8080** — Web interface

## Environment Variables
| Variable | Required | Default | Description |
|----------|----------|---------|-------------|
| `MYSQL_HOST` | Yes | — | MySQL database host |
| `MYSQL_DATABASE` | Yes | — | MySQL database name |
| `MYSQL_USER` | Yes | — | MySQL database user |
| `MYSQL_PASSWORD` | Yes | — | MySQL database password |
| `TZ` | No | UTC | Timezone |

## Volumes
| Volume | Description |
|--------|-------------|
| `nextcloud-data` | User files and data |
| `nextcloud-apps` | Nextcloud apps |
| `nextcloud-config` | Configuration files |

## Docker Compose
```yaml
services:
  nextcloud:
    image: nextcloud:latest
    container_name: nextcloud
    ports:
      - "8080:80"
    environment:
      - MYSQL_HOST=${MYSQL_HOST}
      - MYSQL_DATABASE=${MYSQL_DATABASE}
      - MYSQL_USER=${MYSQL_USER}
      - MYSQL_PASSWORD=${MYSQL_PASSWORD}
      - TZ=${TZ:-UTC}
    volumes:
      - ./nextcloud/data:/var/www/html/data
      - ./nextcloud/apps:/var/www/html/custom_apps
      - ./nextcloud/config:/var/www/html/config
    depends_on:
      - nextcloud-db
    restart: unless-stopped

  nextcloud-db:
    image: postgres:latest
    container_name: nextcloud-db
    environment:
      - POSTGRES_USER=${MYSQL_USER}
      - POSTGRES_PASSWORD=${MYSQL_PASSWORD}
      - POSTGRES_DB=${MYSQL_DATABASE}
    volumes:
      - ./nextcloud/db:/var/lib/postgresql/data
    restart: unless-stopped
```

## Notes
- Access Nextcloud at `http://your-server:8080`
- On first login, create your admin account
- Install apps from the built-in app store (Calendar, Contacts, Deck, Talk, etc.)
- Connect desktop and mobile clients using the server URL
- For production, use a reverse proxy with HTTPS
