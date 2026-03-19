---
id: openclaw
name: OpenClaw
category: container-management
description: AI-native container management platform. Control Docker containers through natural language, Slack, Discord, Telegram, and more.
image: openclaw/openclaw:latest
ports: [18789]
environment:
  - name: OPENCLAW_SECRET_KEY
    description: Secret key for session encryption
    required: false
  - name: OPENCLAW_GATEWAY_URL
    description: Public gateway URL for webhooks
    required: false
  - name: TZ
    description: Timezone
    required: false
    default: UTC
volumes:
  - name: openclaw-data
    description: OpenClaw data directory
    required: true
    default: ./openclaw/data
  - name: docker-socket
    description: Docker socket mount
    required: true
    default: /var/run/docker.sock
---

# OpenClaw

## Description
OpenClaw is an AI-native container management platform. Manage your Docker containers through natural language commands via Slack, Discord, Telegram, Signal, WhatsApp, and more.

## Ports
- **18789** — Web interface and gateway

## Environment Variables
| Variable | Required | Default | Description |
|----------|----------|---------|-------------|
| `OPENCLAW_SECRET_KEY` | No | — | Secret key for session encryption |
| `OPENCLAW_GATEWAY_URL` | No | — | Public gateway URL for webhook callbacks |
| `TZ` | No | UTC | Timezone |

## Volumes
| Volume | Description |
|--------|-------------|
| `openclaw-data` | OpenClaw data and settings |
| `docker-socket` | Docker socket for container management |

## Docker Compose
```yaml
services:
  openclaw:
    image: openclaw/openclaw:latest
    container_name: openclaw
    ports:
      - "18789:18789"
    environment:
      - OPENCLAW_SECRET_KEY=${OPENCLAW_SECRET_KEY}
      - OPENCLAW_GATEWAY_URL=${OPENCLAW_GATEWAY_URL}
      - TZ=${TZ:-UTC}
    volumes:
      - ./openclaw/data:/app/data
      - /var/run/docker.sock:/var/run/docker.sock
    restart: unless-stopped
    privileged: true
```

## Notes
- Access OpenClaw at `http://your-server:18789`
- Connect your messaging platforms (Discord, Slack, Telegram, etc.) from the web UI
- Grant the bot access to channels and it will respond to container management commands
- Example commands: "start nginx", "list all containers", "delete redis"
- The agent can be configured with API keys for programmatic access
- Run `openclaw gateway status` to check the gateway status
