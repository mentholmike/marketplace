---
id: web-check
name: Web-Check
category: utilities
description: All-in-one website recon and analysis tool. Check SSL, DNS, headers, cookies, and 100+ other metrics for any website.
image: alicesec/web-check:latest
ports: [3000]
environment:
  - name: TZ
    description: Timezone
    required: false
    default: UTC
volumes:
  - name: web-check-data
    description: Web-Check data directory
    required: false
    default: ./web-check/data
---

# Web-Check

## Description
Web-Check is an all-in-one website reconnaissance and analysis tool. Enter any URL and get a detailed report on SSL certificates, DNS records, HTTP headers, cookies, open ports, and 100+ other metrics.

## Ports
- **3000** — Web interface

## Environment Variables
| Variable | Required | Default | Description |
|----------|----------|---------|-------------|
| `TZ` | No | UTC | Timezone |

## Volumes
| Volume | Description |
|--------|-------------|
| `web-check-data` | Web-Check data directory (optional) |

## Docker Compose
```yaml
services:
  web-check:
    image: alicesec/web-check:latest
    container_name: web-check
    ports:
      - "3000:3000"
    environment:
      - TZ=${TZ:-UTC}
    volumes:
      - ./web-check/data:/app/data
    restart: unless-stopped
```

## Notes
- Access Web-Check at `http://your-server:3000`
- Enter any URL to get a comprehensive security and configuration report
- Useful for auditing your own servers and checking third-party services
- Reports include: SSL/TLS info, DNS records, WHOIS data, headers, open ports, cookies, redirects, and more
- No API key required — all checks are performed on-demand
