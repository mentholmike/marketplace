---
id: nginx
name: Nginx
category: networking
description: Web server and reverse proxy. Serve websites and route traffic to your Docker containers with SSL support.
image: nginx:latest
ports: [80, 443]
environment:
  - name: TZ
    description: Timezone
    required: false
    default: UTC
volumes:
  - name: nginx-html
    description: Static HTML files
    required: true
    default: ./nginx/html
  - name: nginx-conf
    description: Nginx configuration files
    required: true
    default: ./nginx/conf.d
  - name: nginx-ssl
    description: SSL certificates
    required: false
    default: ./nginx/ssl
---

# Nginx

## Description
Nginx is a web server that can also be used as a reverse proxy, load balancer, and HTTP cache. Serve static sites and route traffic to your Docker containers with automatic SSL.

## Ports
- **80** — HTTP
- **443** — HTTPS

## Environment Variables
| Variable | Required | Default | Description |
|----------|----------|---------|-------------|
| `TZ` | No | UTC | Timezone |

## Volumes
| Volume | Description |
|--------|-------------|
| `nginx-html` | Static HTML files (served at /) |
| `nginx-conf` | Nginx configuration files |
| `nginx-ssl` | SSL certificates (optional) |

## Docker Compose
```yaml
services:
  nginx:
    image: nginx:latest
    container_name: nginx
    ports:
      - "80:80"
      - "443:443"
    environment:
      - TZ=${TZ:-UTC}
    volumes:
      - ./nginx/html:/usr/share/nginx/html
      - ./nginx/conf.d:/etc/nginx/conf.d
      - ./nginx/ssl:/etc/nginx/ssl
    restart: unless-stopped
```

## Notes
- Access Nginx at `http://your-server` (80) or `https://your-server` (443)
- Add site configs in `./nginx/conf.d/` (e.g., `example.com.conf`)
- Example reverse proxy config:
  ```nginx
  server {
    listen 80;
    server_name app.example.com;
    location / {
      proxy_pass http://container-name:port;
    }
  }
  ```
- For SSL, mount certificates to `./nginx/ssl/` or use certbot
