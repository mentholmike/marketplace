---
id: uptime-kuma
name: Uptime Kuma
category: monitoring
description: Self-hosted monitoring tool. Monitor your servers and services with a beautiful dashboard.
image: louislam/uptime-kuma:latest
ports: [3001]
volumes:
  - name: uptime-kuma-data
    description: Uptime Kuma data directory
    required: true
    default: ./uptime-kuma/data
---

# Uptime Kuma

## Description
Uptime Kuma is a fancy self-hosted monitoring tool. Monitor your websites, APIs, and servers with a beautiful dashboard and receive notifications when things go down.

## Ports
- **3001** — Web interface

## Volumes
| Volume | Description |
|--------|-------------|
| `uptime-kuma-data` | Uptime Kuma data and settings |

## Docker Compose
```yaml
services:
  uptime-kuma:
    image: louislam/uptime-kuma:latest
    container_name: uptime-kuma
    ports:
      - "3001:3001"
    volumes:
      - ./uptime-kuma/data:/app/data
      - /var/run/docker.sock:/var/run/docker.sock
    restart: unless-stopped
```

## Notes
- Access Uptime Kuma at `http://your-server:3001`
- On first login, create your admin account
- Add monitors for HTTP, TCP, DNS, and Docker container monitoring
- Configure notification channels (Discord, Telegram, Slack, etc.)
