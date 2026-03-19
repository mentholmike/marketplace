---
id: influxdb
name: InfluxDB
category: database
description: Time series database. Store and query time series data for monitoring and analytics.
image: influxdb:latest
ports: [8086]
environment:
  - name: DOCKER_INFLUXDB_INIT_MODE
    description: Initialization mode
    required: false
    default: setup
  - name: DOCKER_INFLUXDB_INIT_USERNAME
    description: Initial admin username
    required: false
    default: admin
  - name: DOCKER_INFLUXDB_INIT_PASSWORD
    description: Initial admin password
    required: false
    default: adminpassword
  - name: DOCKER_INFLUXDB_INIT_ORG
    description: Initial organization name
    required: false
    default: wagmios
  - name: DOCKER_INFLUXDB_INIT_BUCKET
    description: Initial bucket name
    required: false
    default: metrics
  - name: DOCKER_INFLUXDB_INIT_TOKEN
    description: Initial admin token
    required: false
volumes:
  - name: influxdb-data
    description: InfluxDB data directory
    required: true
    default: ./influxdb/data
---

# InfluxDB

## Description
InfluxDB is an open source time series database optimized for monitoring and analytics. Store and query metrics, events, and real-time analytics.

## Ports
- **8086** — InfluxDB API

## Environment Variables
| Variable | Required | Default | Description |
|----------|----------|---------|-------------|
| `DOCKER_INFLUXDB_INIT_MODE` | No | setup | Initialization mode |
| `DOCKER_INFLUXDB_INIT_USERNAME` | No | admin | Initial admin username |
| `DOCKER_INFLUXDB_INIT_PASSWORD` | No | adminpassword | Initial admin password |
| `DOCKER_INFLUXDB_INIT_ORG` | No | wagmios | Initial organization name |
| `DOCKER_INFLUXDB_INIT_BUCKET` | No | metrics | Initial bucket name |
| `DOCKER_INFLUXDB_INIT_TOKEN` | No | — | Initial admin token |

## Volumes
| Volume | Description |
|--------|-------------|
| `influxdb-data` | InfluxDB data directory |

## Docker Compose
```yaml
services:
  influxdb:
    image: influxdb:latest
    container_name: influxdb
    ports:
      - "8086:8086"
    environment:
      - DOCKER_INFLUXDB_INIT_MODE=setup
      - DOCKER_INFLUXDB_INIT_USERNAME=${DOCKER_INFLUXDB_INIT_USERNAME:-admin}
      - DOCKER_INFLUXDB_INIT_PASSWORD=${DOCKER_INFLUXDB_INIT_PASSWORD:-adminpassword}
      - DOCKER_INFLUXDB_INIT_ORG=${DOCKER_INFLUXDB_INIT_ORG:-wagmios}
      - DOCKER_INFLUXDB_INIT_BUCKET=${DOCKER_INFLUXDB_INIT_BUCKET:-metrics}
      - DOCKER_INFLUXDB_INIT_TOKEN=${DOCKER_INFLUXDB_INIT_TOKEN}
    volumes:
      - ./influxdb/data:/var/lib/influxdb2
    restart: unless-stopped
```

## Notes
- Access InfluxDB at `http://your-server:8086`
- Use InfluxDB clients or the CLI to write and query data
- Telegraf can be used as a collector to send metrics to InfluxDB
- Grafana can connect to InfluxDB as a data source
