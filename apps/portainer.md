---
id: portainer
name: Portainer
category: container-management
description: Container management made easy. Web interface for managing Docker containers and stacks.
image: portainer/portainer-ce:latest
ports: [9000, 8000]
volumes:
  - name: portainer-data
    description: Portainer data directory
    required: true
    default: ./portainer/data
---

# Portainer

## Description
Portainer is a lightweight management UI for Docker. Manage your containers, images, networks, volumes, and stacks through a simple web interface.

## Ports
- **9000** — Web interface
- **8000** — Portainer agent (for remote management)

## Volumes
| Volume | Description |
|--------|-------------|
| `portainer-data` | Portainer data and settings |

## Docker Compose
```yaml
services:
  portainer:
    image: portainer/portainer-ce:latest
    container_name: portainer
    ports:
      - "9000:9000"
      - "8000:8000"
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock
      - ./portainer/data:/data
    restart: unless-stopped
```

## Notes
- Access Portainer at `http://your-server:9000`
- On first login, create your admin account
- Connect to the local Docker socket for full container management
- For remote Docker hosts, use the agent on port 8000
