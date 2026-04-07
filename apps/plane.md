---
id: plane
name: Plane
category: Productivity
description: Open source project management platform. Track issues, sprints, and roadmaps for your team without enterprise pricing.
image: makeplane/plane-frontend:latest
ports: [6080]
---

# Plane

## Description
Open source project management platform. Track issues, sprints, and roadmaps for your team without enterprise pricing.

## Ports
- **6080 — Web interface**

## Docker Compose
```yaml
services:
  plane:
    image: makeplane/plane-frontend:latest
    container_name: plane
    volumes:
      - ./plane/data:/data
    ports:
      - "6080:6080"
    restart: unless-stopped
```
