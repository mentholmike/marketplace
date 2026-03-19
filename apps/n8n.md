---
id: n8n
name: n8n
category: productivity
description: Workflow automation tool. Automate tasks between apps with a visual workflow editor.
image: n8nio/n8n:latest
ports: [5678]
environment:
  - name: N8N_BASIC_AUTH_ACTIVE
    description: Enable basic authentication
    required: false
    default: "true"
  - name: N8N_BASIC_AUTH_USER
    description: Basic auth username
    required: false
    default: admin
  - name: N8N_BASIC_AUTH_PASSWORD
    description: Basic auth password
    required: false
    default: admin
  - name: N8N_HOST
    description: Hostname for webhooks
    required: false
    default: localhost
  - name: TZ
    description: Timezone
    required: false
    default: UTC
volumes:
  - name: n8n-data
    description: n8n data directory
    required: true
    default: ./n8n/data
---

# n8n

## Description
n8n is a workflow automation tool that lets you connect apps and automate tasks with a visual drag-and-drop workflow editor.

## Ports
- **5678** — Web interface

## Environment Variables
| Variable | Required | Default | Description |
|----------|----------|---------|-------------|
| `N8N_BASIC_AUTH_ACTIVE` | No | true | Enable basic authentication |
| `N8N_BASIC_AUTH_USER` | No | admin | Basic auth username |
| `N8N_BASIC_AUTH_PASSWORD` | No | admin | Basic auth password |
| `N8N_HOST` | No | localhost | Hostname for webhooks |
| `TZ` | No | UTC | Timezone |

## Volumes
| Volume | Description |
|--------|-------------|
| `n8n-data` | n8n data and workflows |

## Docker Compose
```yaml
services:
  n8n:
    image: n8nio/n8n:latest
    container_name: n8n
    ports:
      - "5678:5678"
    environment:
      - N8N_BASIC_AUTH_ACTIVE=${N8N_BASIC_AUTH_ACTIVE:-true}
      - N8N_BASIC_AUTH_USER=${N8N_BASIC_AUTH_USER:-admin}
      - N8N_BASIC_AUTH_PASSWORD=${N8N_BASIC_AUTH_PASSWORD:-admin}
      - N8N_HOST=${N8N_HOST:-localhost}
      - TZ=${TZ:-UTC}
    volumes:
      - ./n8n/data:/home/node/.n8n
    restart: unless-stopped
```

## Notes
- Access n8n at `http://your-server:5678`
- Create workflows by connecting nodes together
- n8n supports webhooks, scheduled triggers, and manual triggers
- Integrate with 400+ apps including Slack, GitHub, Notion, etc.
