---
id: immich
name: Immich
category: photo-video
description: Self-hosted photo and video backup solution. Automatically backs up your photos and videos from your phone to your server.
image: ghcr.io/immich-app/immich-server:latest
ports: [2283]
environment:
  - name: DB_PASSWORD
    description: PostgreSQL database password
    required: true
  - name: REDIS_PASSWORD
    description: Redis cache password
    required: false
  - name: TZ
    description: Timezone
    required: false
    default: UTC
volumes:
  - name: uploads
    description: Uploaded photos and videos
    required: true
    default: ./immich/uploads
  - name: db-data
    description: PostgreSQL database
    required: true
    default: ./immich/db
  - name: redis-data
    description: Redis cache
    required: true
    default: ./immich/redis
---

# Immich

## Description
Immich is a self-hosted photo and video backup solution. It automatically backs up your photos and videos from your phone, similar to Google Photos but fully under your control.

## Ports
- **2283** — Web interface

## Environment Variables
| Variable | Required | Default | Description |
|----------|----------|---------|-------------|
| `DB_PASSWORD` | Yes | — | PostgreSQL database password |
| `REDIS_PASSWORD` | No | — | Redis cache password |
| `TZ` | No | UTC | Timezone |

## Volumes
| Volume | Description |
|--------|-------------|
| `uploads` | Uploaded photos and videos |
| `db-data` | PostgreSQL database |
| `redis-data` | Redis cache |

## Docker Compose
```yaml
services:
  immich:
    image: ghcr.io/immich-app/immich-server:latest
    container_name: immich
    command: ['start.sh', 'immich']
    ports:
      - "2283:3001"
    environment:
      - DB_PASSWORD=${DB_PASSWORD}
      - REDIS_PASSWORD=${REDIS_PASSWORD}
      - TZ=${TZ:-UTC}
      - DB_HOSTNAME=immich-db
      - REDIS_HOSTNAME=immich-redis
    volumes:
      - ./immich/uploads:/usr/src/app/upload
      - /etc/localtime:/etc/localtime:ro
    depends_on:
      - immich-db
      - immich-redis
    restart: unless-stopped

  immich-db:
    image: tensorchord/pgvecto-rs:pg16-v0.2.0
    container_name: immich-db
    environment:
      - POSTGRES_PASSWORD=${DB_PASSWORD}
      - POSTGRES_USER=immich
      - POSTGRES_DB=immich
    volumes:
      - ./immich/db:/var/lib/postgresql/data
    restart: unless-stopped

  immich-redis:
    image: redis:6.2-alpine
    container_name: immich-redis
    environment:
      - REDIS_PASSWORD=${REDIS_PASSWORD}
    volumes:
      - ./immich/redis:/data
    restart: unless-stopped
```

## Notes
- Download the Immich mobile app (iOS/Android) to auto-backup your photos
- First run requires creating an admin account via the web UI
- Recommended to run on a machine with plenty of storage
- Use the mobile app to configure backup settings and albums
