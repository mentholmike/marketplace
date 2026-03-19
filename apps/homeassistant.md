---
id: homeassistant
name: Home Assistant
category: home-automation
description: Open source home automation platform focused on privacy and local control.
image: homeassistant/home-assistant:latest
ports: [8123]
environment:
  - name: TZ
    description: Timezone
    required: false
    default: UTC
volumes:
  - name: config
    description: Home Assistant configuration directory
    required: true
    default: ./homeassistant/config
---

# Home Assistant

## Description
Home Assistant is an open source home automation platform that puts local control and privacy first. Connect all your smart devices in one place.

## Ports
- **8123** — Web interface

## Environment Variables
| Variable | Required | Default | Description |
|----------|----------|---------|-------------|
| `TZ` | No | UTC | Timezone |

## Volumes
| Volume | Description |
|--------|-------------|
| `config` | Home Assistant configuration |

## Docker Compose
```yaml
services:
  homeassistant:
    image: homeassistant/home-assistant:latest
    container_name: homeassistant
    ports:
      - "8123:8123"
    environment:
      - TZ=${TZ:-UTC}
    volumes:
      - ./homeassistant/config:/config
      - /etc/localtime:/etc/localtime:ro
    restart: unless-stopped
    network_mode: host
```

## Notes
- Access Home Assistant at `http://your-server:8123`
- On first login, create your admin account
- Add integrations from Configuration → Devices & Services
- For Docker network mode, use `network_mode: host` to allow discovery
