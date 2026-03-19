---
id: prometheus
name: Prometheus
category: monitoring
description: Monitoring system and time series database. Collects and stores metrics from configured targets.
image: prom/prometheus:latest
ports: [9090]
environment:
  - name: TZ
    description: Timezone
    required: false
    default: UTC
volumes:
  - name: config
    description: Prometheus configuration directory
    required: true
    default: ./prometheus/config
  - name: data
    description: Prometheus data directory
    required: true
    default: ./prometheus/data
---

# Prometheus

## Description
Prometheus is an open source monitoring system and time series database. It collects and stores metrics from configured targets at regular intervals.

## Ports
- **9090** — Web interface

## Environment Variables
| Variable | Required | Default | Description |
|----------|----------|---------|-------------|
| `TZ` | No | UTC | Timezone |

## Volumes
| Volume | Description |
|--------|-------------|
| `config` | Prometheus configuration |
| `data` | Prometheus time series database |

## Docker Compose
```yaml
services:
  prometheus:
    image: prom/prometheus:latest
    container_name: prometheus
    ports:
      - "9090:9090"
    environment:
      - TZ=${TZ:-UTC}
    volumes:
      - ./prometheus/config:/etc/prometheus
      - ./prometheus/data:/prometheus
    command:
      - '--config.file=/etc/prometheus/prometheus.yml'
      - '--storage.tsdb.path=/prometheus'
    restart: unless-stopped
```

## Notes
- Access Prometheus at `http://your-server:9090`
- Configure scrape targets in `prometheus.yml`
- Common targets: node-exporter, cadvisor, your application
- Grafana can connect to Prometheus as a data source
