---
id: vaultwarden
name: Vaultwarden
category: security
description: Bitwarden compatible password manager. Self-hosted alternative to Bitwarden, written in Rust.
image: vaultwarden/server:latest
ports: [80]
environment:
  - name: SIGNUP_ALLOWED
    description: Allow new user registrations
    required: false
    default: "true"
  - name: ADMIN_TOKEN
    description: Admin panel access token (generate with: openssl rand -base64 48)
    required: false
  - name: TZ
    description: Timezone
    required: false
    default: UTC
volumes:
  - name: data
    description: Vaultwarden data directory
    required: true
    default: ./vaultwarden/data
---

# Vaultwarden

## Description
Vaultwarden is a self-hosted Bitwarden compatible password manager. Store passwords, secure notes, and sensitive data with end-to-end encryption.

## Ports
- **80** — Web interface

## Environment Variables
| Variable | Required | Default | Description |
|----------|----------|---------|-------------|
| `SIGNUP_ALLOWED` | No | true | Allow new user registrations |
| `ADMIN_TOKEN` | No | — | Admin panel access token |
| `TZ` | No | UTC | Timezone |

## Volumes
| Volume | Description |
|--------|-------------|
| `data` | Vaultwarden data directory |

## Docker Compose
```yaml
services:
  vaultwarden:
    image: vaultwarden/server:latest
    container_name: vaultwarden
    ports:
      - "80:80"
    environment:
      - SIGNUP_ALLOWED=${SIGNUP_ALLOWED:-true}
      - ADMIN_TOKEN=${ADMIN_TOKEN}
      - TZ=${TZ:-UTC}
    volumes:
      - ./vaultwarden/data:/data
    restart: unless-stopped
```

## Notes
- Access the web vault at `http://your-server`
- Use Bitwarden clients (browser extension, mobile app) by connecting to your self-hosted server
- Generate an admin token with: `openssl rand -base64 48`
- Disable signup after creating your account: `SIGNUP_ALLOWED=false`
- For production, use a reverse proxy (Nginx, Caddy) with HTTPS
