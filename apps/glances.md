---
id: glances
name: Glances
category: monitoring
description: Cross-platform system monitoring tool. Monitor CPU, memory, disk, network, and processes in real-time.
image: nicolargo/glances:latest
ports: [61208]
environment:
  - name: TZ
    description: Timezone
    required: false
    default: UTC
  - name: GLANCES_OPT
    description: Additional Glances options
    required: false
volumes:
  - name: glances-conf
    description: Glances configuration directory
    required: false
    default: ./glances/conf
---

# Glances

## Description
Glances is a cross-platform system monitoring tool written in Python. Monitor CPU, memory, disk I/O, network, and processes in real-time.

## Ports
- **61208** — Web interface

## Environment Variables
| Variable | Required | Default | Description |
|----------|----------|---------|-------------|
| `TZ` | No | UTC | Timezone |
| `GLANCES_OPT` | No | — | Additional Glances command line options |

## Volumes
| Volume | Description |
|--------|-------------|
| `glances-conf` | Glances configuration (optional) |

## Docker Compose
```yaml
services:
  glances:
    image: nicolargo/glances:latest
    container_name: glances
    ports:
      - "61208:61208"
    environment:
      - TZ=${TZ:-UTC}
      - GLANCES_OPT=${GLANCES_OPT}
    volumes:
      - ./glances/conf:/root/.config/glances
    restart: unless-stopped
```

## Notes
- Access Glances at `http://your-server:61208`
- For per-CPU stats, add `GLANCES_OPT=-w` to enable web server mode
- Glances can also be accessed via terminal: `docker exec -it glances glances`
