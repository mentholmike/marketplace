---
id: gluetun
name: Gluetun
category: vpn
description: VPN container for routing Docker services through WireGuard or OpenVPN. Run any container's traffic through a VPN.
image: qmcgaw/gluetun:latest
ports: [8888, 8388, 8388]
environment:
  - name: VPN_SERVICE_PROVIDER
    description: VPN provider (mullvad, nordvpn, surfshark, etc.)
    required: true
  - name: OPENVPN_USERNAME
    description: OpenVPN username
    required: false
  - name: OPENVPN_PASSWORD
    description: OpenVPN password
    required: false
  - name: WIREGUARD_PRIVATE_KEY
    description: WireGuard private key
    required: false
  - name: WIREGUARD_ADDRESSES
    description: WireGuard interface addresses
    required: false
  - name: TZ
    description: Timezone
    required: false
    default: UTC
volumes:
  - name: gluetun-data
    description: Gluetun configuration and state
    required: true
    default: ./gluetun
---

# Gluetun

## Description
Gluetun is a VPN container that routes other containers' traffic through WireGuard or OpenVPN. Run Plex, Sonarr, Radarr, or any service through your VPN with a single environment variable change.

## Ports
- **8888** — HTTP proxy
- **8388** — Shadowsocks (if enabled)
- **8388** — Built-in VPN (if built-in)

## Environment Variables
| Variable | Required | Default | Description |
|----------|----------|---------|-------------|
| `VPN_SERVICE_PROVIDER` | Yes | — | VPN provider (mullvad, nordvpn, surfshark, etc.) |
| `OPENVPN_USERNAME` | No | — | OpenVPN username |
| `OPENVPN_PASSWORD` | No | — | OpenVPN password |
| `WIREGUARD_PRIVATE_KEY` | No | — | WireGuard private key |
| `WIREGUARD_ADDRESSES` | No | — | WireGuard interface addresses |
| `TZ` | No | UTC | Timezone |

## Volumes
| Volume | Description |
|--------|-------------|
| `gluetun-data` | Gluetun configuration and state |

## Docker Compose
```yaml
services:
  gluetun:
    image: qmcgaw/gluetun:latest
    container_name: gluetun
    cap_add:
      - NET_ADMIN
    environment:
      - VPN_SERVICE_PROVIDER=${VPN_SERVICE_PROVIDER}
      - OPENVPN_USERNAME=${OPENVPN_USERNAME}
      - OPENVPN_PASSWORD=${OPENVPN_PASSWORD}
      - WIREGUARD_PRIVATE_KEY=${WIREGUARD_PRIVATE_KEY}
      - WIREGUARD_ADDRESSES=${WIREGUARD_ADDRESSES}
      - TZ=${TZ:-UTC}
    volumes:
      - ./gluetun:/gluetun
    ports:
      - "8888:8888"
      - "8388:8388"
    restart: unless-stopped
```

## Notes
- Gluetun creates a network that other containers join
- Wire to other containers: `network_mode: service:gluetun`
- Use with Plex, Radarr, Sonarr,Transmission, qBittorrent, etc.
- Requires a VPN subscription (Mullvad, NordVPN, etc.)
- For Mullvad WireGuard: set `VPN_SERVICE_PROVIDER=mullvad` and WireGuard keys
