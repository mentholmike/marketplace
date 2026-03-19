---
id: novu
name: Novu
category: notifications
description: Open source notification infrastructure. Send transactional emails, SMS, push, and in-app notifications from a single API.
image: novu:latest
ports: [3000, 3001]
environment:
  - name: POSTGRES_PASSWORD
    description: PostgreSQL database password
    required: true
  - name: REDIS_HOST
    description: Redis host
    required: false
    default: localhost
  - name: REDIS_PORT
    description: Redis port
    required: false
    default: "6379"
  - name: REDIS_PASSWORD
    description: Redis password
    required: false
  - name: TZ
    description: Timezone
    required: false
    default: UTC
volumes:
  - name: novu-data
    description: Novu data directory
    required: true
    default: ./novu/data
---

# Novu

## Description
Novu is an open source notification infrastructure. Send transactional notifications via email, SMS, push, and in-app — all through a single API. Monitor delivery and manage preferences from a dashboard.

## Ports
- **3000** — Web dashboard
- **3001** — API

## Environment Variables
| Variable | Required | Default | Description |
|----------|----------|---------|-------------|
| `POSTGRES_PASSWORD` | Yes | — | PostgreSQL database password |
| `REDIS_HOST` | No | localhost | Redis host |
| `REDIS_PORT` | No | 6379 | Redis port |
| `REDIS_PASSWORD` | No | — | Redis password |
| `TZ` | No | UTC | Timezone |

## Volumes
| Volume | Description |
|--------|-------------|
| `novu-data` | Novu data directory |

## Docker Compose
```yaml
services:
  novu-api:
    image: novu:latest
    container_name: novu-api
    command: start:api
    ports:
      - "3001:3001"
    environment:
      - POSTGRES_PASSWORD=${POSTGRES_PASSWORD}
      - REDIS_HOST=${REDIS_HOST:-localhost}
      - REDIS_PORT=${REDIS_PORT:-6379}
      - REDIS_PASSWORD=${REDIS_PASSWORD}
      - TZ=${TZ:-UTC}
      - STORE_ENCRYPTION_KEY=your-32-char-random-key
    volumes:
      - ./novu/data:/app/data
    depends_on:
      - novu-db
      - novu-redis
    restart: unless-stopped

  novu-web:
    image: novu/novu:latest
    container_name: novu-web
    command: start:web
    ports:
      - "3000:3000"
    environment:
      - REACT_APP_API_URL=http://localhost:3001
      - REACT_APP_WIDGET_URL=http://localhost:3002
    restart: unless-stopped

  novu-db:
    image: postgres:latest
    container_name: novu-db
    environment:
      - POSTGRES_PASSWORD=${POSTGRES_PASSWORD}
      - POSTGRES_USER=novu
      - POSTGRES_DB=novu
    volumes:
      - ./novu/db:/var/lib/postgresql/data
    restart: unless-stopped

  novu-redis:
    image: redis:6.2-alpine
    container_name: novu-redis
    environment:
      - REDIS_PASSWORD=${REDIS_PASSWORD}
    volumes:
      - ./novu/redis:/data
    restart: unless-stopped

  novu-worker:
    image: novu:latest
    container_name: novu-worker
    command: start:worker
    environment:
      - POSTGRES_PASSWORD=${POSTGRES_PASSWORD}
      - REDIS_HOST=novu-redis
      - REDIS_PORT=${REDIS_PORT:-6379}
      - REDIS_PASSWORD=${REDIS_PASSWORD}
      - TZ=${TZ:-UTC}
      - STORE_ENCRYPTION_KEY=your-32-char-random-key
    volumes:
      - ./novu/data:/app/data
    depends_on:
      - novu-db
      - novu-redis
    restart: unless-stopped

  novu-ws:
    image: novu:latest
    container_name: novu-ws
    command: start:ws
    ports:
      - "3002:3002"
    environment:
      - REDIS_HOST=novu-redis
      - REDIS_PORT=${REDIS_PORT:-6379}
      - REDIS_PASSWORD=${REDIS_PASSWORD}
    depends_on:
      - novu-redis
    restart: unless-stopped
```

## Notes
- Access the Novu dashboard at `http://your-server:3000`
- Set `STORE_ENCRYPTION_KEY` to a random 32-character string in production
- Configure email (SendGrid, Mailgun, SES), SMS (Twilio), and push providers in settings
- Use the API to trigger notifications: `POST /v1/events/trigger`
- Novu handles subscriber management, notification preferences, and delivery tracking
