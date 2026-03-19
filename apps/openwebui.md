---
id: openwebui
name: Open WebUI
category: ai-ml
description: User-friendly WebUI for AI models. Chat with Ollama and other LLMs through a clean, open source interface.
image: ghcr.io/open-webui/open-webui:main
ports: [8080]
environment:
  - name: OLLAMA_BASE_URL
    description: Ollama server URL
    required: false
    default: http://localhost:11434
  - name: WEBUI_SECRET_KEY
    description: Secret key for sessions
    required: false
  - name: TZ
    description: Timezone
    required: false
    default: UTC
volumes:
  - name: webui-data
    description: Open WebUI data directory
    required: true
    default: ./openwebui/data
---

# Open WebUI

## Description
Open WebUI is a feature-rich, self-hosted WebUI for AI models. Works with Ollama, and also supports OpenAI-compatible APIs. Features chat history, image upload, code execution, and more.

## Ports
- **8080** — Web interface

## Environment Variables
| Variable | Required | Default | Description |
|----------|----------|---------|-------------|
| `OLLAMA_BASE_URL` | No | http://localhost:11434 | Ollama server URL |
| `WEBUI_SECRET_KEY` | No | — | Secret key for sessions |
| `TZ` | No | UTC | Timezone |

## Volumes
| Volume | Description |
|--------|-------------|
| `webui-data` | Open WebUI data and settings |

## Docker Compose
```yaml
services:
  openwebui:
    image: ghcr.io/open-webui/open-webui:main
    container_name: openwebui
    ports:
      - "8080:8080"
    environment:
      - OLLAMA_BASE_URL=${OLLAMA_BASE_URL:-http://localhost:11434}
      - WEBUI_SECRET_KEY=${WEBUI_SECRET_KEY}
      - TZ=${TZ:-UTC}
    volumes:
      - ./openwebui/data:/app/backend/data
    restart: unless-stopped
```

## Notes
- Access Open WebUI at `http://your-server:8080`
- Connect to Ollama running locally or on another server
- Supports multiple AI models — select from the model dropdown
- Enable image upload in settings for vision tasks
- Create accounts and manage users in the admin panel
