---
id: minecraft
name: Minecraft Server
category: gaming
description: Minecraft Java Edition Server. Host your own multiplayer Minecraft world.
image: itzg/minecraft-server:latest
ports: [25565]
environment:
  - name: EULA
    description: Accept Mojang EULA
    required: true
    value: "TRUE"
  - name: MEMORY
    description: Server memory allocation
    required: false
    default: 2G
  - name: VERSION
    description: Minecraft version
    required: false
    default: LATEST
  - name: MODE
    description: Game mode (survival, creative, adventure, spectator)
    required: false
    default: survival
volumes:
  - name: data
    description: Minecraft world data
    required: true
    default: ./minecraft/data
---

# Minecraft Server

## Description
Run your own Minecraft Java Edition server for multiplayer gaming with friends.

## Ports
- **25565** — Minecraft game server

## Environment Variables
| Variable | Required | Default | Description |
|----------|----------|---------|-------------|
| `EULA` | Yes | TRUE | Must be "TRUE" to accept Mojang EULA |
| `MEMORY` | No | 2G | Server memory allocation |
| `VERSION` | No | LATEST | Minecraft version |
| `MODE` | No | survival | Game mode |

## Volumes
| Volume | Description |
|--------|-------------|
| `data` | Minecraft world data |

## Docker Compose
```yaml
services:
  minecraft:
    image: itzg/minecraft-server:latest
    container_name: minecraft
    ports:
      - "25565:25565"
    environment:
      - EULA=TRUE
      - MEMORY=${MEMORY:-2G}
      - VERSION=${VERSION:-LATEST}
      - MODE=${MODE:-survival}
    volumes:
      - ./minecraft/data:/data
    restart: unless-stopped
```

## Notes
- Players connect to `your-server-ip:25565`
- For paper server, set `TYPE=PAPER` environment variable
- Set `ONLINE_MODE=FALSE` to allow cracked clients (not recommended)
- Back up the `./minecraft/data` directory regularly
