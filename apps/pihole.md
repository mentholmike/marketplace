---
id: pihole
name: Pi-hole
category: networking
description: Network-wide ad blocking. Block ads on your entire network at the DNS level.
image: pihole/pihole:latest
ports: [80, 53]
environment:
  - name: TZ
    description: Timezone
    required: false
    default: UTC
  - name: WEBPASSWORD
    description: Admin web interface password
    required: false
  - name: DNSMASQ_LISTENING
    description: DNSmasq listening interface
    required: false
    default: local
volumes:
  - name: etc-dnsmasq
    description: DNSmasq configuration directory
    required: true
    default: ./pihole/etc-dnsmasq
  - name: etc-pihole
    description: Pi-hole configuration directory
    required: true
    default: ./pihole/etc-pihole
---

# Pi-hole

## Description
Pi-hole is a network-wide ad blocker that blocks ads at the DNS level. All devices on your network can benefit from ad-free browsing without client-side software.

## Ports
- **80** — Web interface (HTTP)
- **53** — DNS server (TCP/UDP)

## Environment Variables
| Variable | Required | Default | Description |
|----------|----------|---------|-------------|
| `TZ` | No | UTC | Timezone |
| `WEBPASSWORD` | No | — | Admin web interface password |
| `DNSMASQ_LISTENING` | No | local | Which interface DNSmasq listens on |

## Volumes
| Volume | Description |
|--------|-------------|
| `etc-dnsmasq` | DNSmasq configuration |
| `etc-pihole` | Pi-hole configuration and blocklists |

## Docker Compose
```yaml
services:
  pihole:
    image: pihole/pihole:latest
    container_name: pihole
    ports:
      - "53:53/tcp"
      - "53:53/udp"
      - "80:80/tcp"
    environment:
      - TZ=${TZ:-UTC}
      - WEBPASSWORD=${WEBPASSWORD}
      - DNSMASQ_LISTENING=local
    volumes:
      - ./pihole/etc-pihole:/etc/pihole
      - ./pihole/etc-dnsmasq:/etc/dnsmasq.d
    restart: unless-stopped
    network_mode: host
```

## Notes
- Set your router's DNS to your server's IP to route all DNS through Pi-hole
- Access the admin interface at `http://your-server/admin`
- Change the DNS upstream servers in Settings if needed (default: Google DNS)
- Add custom blocklists in the admin interface
