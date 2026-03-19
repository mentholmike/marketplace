---
id: wireguard
name: WireGuard
category: vpn
description: Fast and secure VPN. Modern VPN protocol with simple setup and excellent performance.
image: linuxserver/wireguard:latest
ports: [51820]
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
  - name: config
    description: WireGuard configuration directory
    required: true
    default: ./wireguard/config
---

# WireGuard

## Description
WireGuard is a modern VPN protocol with a focus on simplicity and security. Fast, efficient, and easier to configure than OpenVPN.

## Ports
- **51820** — WireGuard VPN (UDP)

## Environment Variables
| Variable | Required | Default | Description |
|----------|----------|---------|-------------|
| `PUID` | No | 1000 | User ID for file permissions |
| `PGID` | No | 1000 | Group ID for file permissions |
| `TZ` | No | UTC | Timezone |

## Volumes
| Volume | Description |
|--------|-------------|
| `config` | WireGuard configuration and keys |

## Docker Compose
```yaml
services:
  wireguard:
    image: linuxserver/wireguard:latest
    container_name: wireguard
    cap_add:
      - NET_ADMIN
      - SYS_MODULE
    ports:
      - "51820:51820/udp"
    environment:
      - PUID=${PUID:-1000}
      - PGID=${PGID:-1000}
      - TZ=${TZ:-UTC}
    volumes:
      - ./wireguard/config:/config
      - /lib/modules:/lib/modules:ro
    restart: unless-stopped
    sysctls:
      - net.ipv4.conf.all.src_valid_mark=1
```

## Notes
- Download the WireGuard app on your devices from wireguard.com/install
- Generate client configs from the web UI or using `wg genkey` / `wg pubkey`
- Each client needs a unique private/public key pair
- Share the server's public key and client's config to connect
