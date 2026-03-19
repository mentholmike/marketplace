---
id: ollama
name: Ollama
category: ai-ml
description: Self-hosted AI model runner. Run Llama, Mistral, and other open-source AI models locally.
image: ollama/ollama:latest
ports: [11434]
environment:
  - name: OLLAMA_HOST
    description: Host to bind to
    required: false
    default: 0.0.0.0
  - name: OLLAMA_MODELS
    description: Path to models directory
    required: false
    default: /root/.ollama
volumes:
  - name: ollama-data
    description: Ollama models and data
    required: true
    default: ./ollama/data
---

# Ollama

## Description
Ollama lets you run open-source AI models locally including Llama 2, Mistral, CodeLlama, and more. No API keys needed, fully offline.

## Ports
- **11434** — API interface

## Environment Variables
| Variable | Required | Default | Description |
|----------|----------|---------|-------------|
| `OLLAMA_HOST` | No | 0.0.0.0 | Host to bind to |
| `OLLAMA_MODELS` | No | /root/.ollama | Path to models directory |

## Volumes
| Volume | Description |
|--------|-------------|
| `ollama-data` | Ollama models and data |

## Docker Compose
```yaml
services:
  ollama:
    image: ollama/ollama:latest
    container_name: ollama
    network_mode: host
    environment:
      - OLLAMA_HOST=${OLLAMA_HOST:-0.0.0.0}
    volumes:
      - ./ollama/data:/root/.ollama
    restart: unless-stopped
```

## Notes
- Use `ollama pull <model>` to download models (e.g., `ollama pull llama2`)
- API base URL within container: `http://localhost:11434`
- For GPU access, add `--gpus all` flag and install nvidia-container-toolkit
- Web UIs like Open WebUI can connect to Ollama as a backend
