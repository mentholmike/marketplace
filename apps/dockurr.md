---
id: dockurr
name: Dockurr
category: container-management
description: Docker container builder and runner with a web interface. Build, run, and manage containers through a simple browser UI.
image: dockurr/dockurr:latest
ports: [8080]
environment:
  - name: TZ
    description: Timezone
    required: false
    default: UTC
volumes:
  - name: dockurr-data
    description: Dockurr data directory
    required: true
    default: ./dockurr/data
  - name: docker-socket
    description: Docker socket
    required: true
    default: /var/run/docker.sock
---

# Dockurr

## Description
Dockurr is a web-based Docker container builder and runner. Search for any Docker image, configure it through a simple UI, and run it without touching the command line.

## Ports
- **8080** — Web interface

## Environment Variables
| Variable | Required | Default | Description |
|----------|----------|---------|-------------|
| `TZ` | No | UTC | Timezone |

## Volumes
| Volume | Description |
|--------|-------------|
| `dockurr-data` | Dockurr data directory |
| `docker-socket` | Docker socket for container management |

## Docker Compose
```yaml
services:
  dockurr:
    image: dockurr/dockurr:latest
    container_name: dockurr
    ports:
      - "8080:8080"
    environment:
      - TZ=${TZ:-UTC}
    volumes:
      - ./dockurr/data:/data
      - /var/run/docker.sock:/var/run/docker.sock
    restart: unless-stopped
    privileged: true
```

## Notes
- Access Dockurr at `http://your-server:8080`
- Search for any public Docker image
- Configure environment variables and ports through the web UI
- Build custom images using Dockerfile support
- View logs and container status in real-time
