---
id: grafana
name: Grafana
category: analytics
description: Analytics and monitoring solution. Visualize metrics, logs, and traces in customizable dashboards.
image: grafana/grafana:latest
ports: [3000]
environment:
  - name: GF_SECURITY_ADMIN_USER
    description: Admin username
    required: false
    default: admin
  - name: GF_SECURITY_ADMIN_PASSWORD
    description: Admin password
    required: false
    default: admin
  - name: GF_INSTALL_PLUGINS
    description: Comma-separated list of plugins to install
    required: false
volumes:
  - name: grafana-data
    description: Grafana data directory
    required: true
    default: ./grafana/data
---

# Grafana

## Description
Grafana is an open source analytics and monitoring solution. Create custom dashboards to visualize metrics from Prometheus, InfluxDB, and other data sources.

## Ports
- **3000** — Web interface

## Environment Variables
| Variable | Required | Default | Description |
|----------|----------|---------|-------------|
| `GF_SECURITY_ADMIN_USER` | No | admin | Admin username |
| `GF_SECURITY_ADMIN_PASSWORD` | No | admin | Admin password |
| `GF_INSTALL_PLUGINS` | No | — | Comma-separated list of plugins to install |

## Volumes
| Volume | Description |
|--------|-------------|
| `grafana-data` | Grafana data and dashboards |

## Docker Compose
```yaml
services:
  grafana:
    image: grafana/grafana:latest
    container_name: grafana
    ports:
      - "3000:3000"
    environment:
      - GF_SECURITY_ADMIN_USER=${GF_SECURITY_ADMIN_USER:-admin}
      - GF_SECURITY_ADMIN_PASSWORD=${GF_SECURITY_ADMIN_PASSWORD:-admin}
      - GF_INSTALL_PLUGINS=${GF_INSTALL_PLUGINS}
    volumes:
      - ./grafana/data:/var/lib/grafana
    restart: unless-stopped
```

## Notes
- Access Grafana at `http://your-server:3000` (default login: admin/admin)
- Add Prometheus as a data source: Settings → Data Sources → Prometheus
- Import dashboards from [grafana.com/dashboards](https://grafana.com/dashboards)
- Change the default admin password after first login
