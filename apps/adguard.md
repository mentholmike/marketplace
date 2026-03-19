---
id: adguard
name: AdGuard Home
category: networking
description: Network-wide ad blocker with DNS customization. Similar to Pi-hole with a modern web interface.
image: adguard/adguardhome:latest
ports: [53, 853, 3000, 80]
environment:
  - name: TZ
    description: Timezone
    required: false
    default: UTC
volumes:
  - name: work
    description: AdGuard work directory
    required: true
    default: ./adguard/work
  - name: config
    description: AdGuard configuration directory
    required: true
    default: ./adguard/config
---

# AdGuard Home

## Description
AdGuard Home is a network-wide ad blocker and DNS resolver. Block ads, trackers, and malicious domains across your entire network.

## Ports
- **53** — DNS server (TCP/UDP)
- **853** — DNS-over-TLS
- **80** — Web interface (HTTP)
- **3000** — Web interface alternative

## Environment Variables
| Variable | Required | Default | Description |
|----------|----------|---------|-------------|
| `TZ` | No | UTC | Timezone |

## Volumes
| Volume | Description |
|--------|-------------|
| `work` | AdGuard work directory |
| `config` | AdGuard configuration |

## Docker Compose
```yaml
services:
  adguardhome:
    image: adguard/adguardhome:latest
    container_name: adguardhome
    ports:
      - "53:53/tcp"
      - "53:53/udp"
      - "853:853/tcp"
      - "80:80/tcp"
      - "3000:3000/tcp"
    environment:
      - TZ=${TZ:-UTC}
    volumes:
      - ./adguard/work:/opt/adguardhome/work
      - ./adguard/config:/opt/adguardhome/conf
    restart: unless-stopped
```

## Notes
- Access AdGuard Home at `http://your-server:3000`
- Set your router's DNS to your server's IP
- Configure upstream DNS servers in Settings (default: Cloudflare)
- Enable DNS-over-TLS and DNS-over-HTTPS for encrypted DNS
