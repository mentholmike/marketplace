# Wagmios Marketplace

Self-hosted app marketplace for [Wagmios](https://github.com/mentholmike/wagmios) — a Docker container management dashboard with AI agent support.

## Overview

This marketplace contains pre-configured Docker Compose templates for popular self-hosted applications. Each app is defined as a simple markdown file that AI agents can read to install services on your server.

## For Users

Browse available apps at the docs site (coming soon). Each app shows:
- Description and category
- Default port
- Required and optional configuration

Ask your Wagmios agent to install any app from the marketplace.

## For AI Agents

### Fetching the marketplace

```
GET /api/marketplace
```
Returns the manifest with all available apps.

### Getting an app template

```
GET /api/marketplace/{app-id}
```
Returns the app's markdown file with the full Docker Compose template.

### Installing an app

```
POST /api/marketplace/install
Content-Type: application/json

{
  "app_id": "homeassistant",
  "custom_name": "my-homeassistant",
  "environment": {
    "TZ": "America/New_York"
  },
  "volumes": {
    "config": "./my-homeassistant/config"
  }
}
```

The agent fills in user preferences, submits, and the human approves in the Wagmios dashboard before the app is installed.

## App Structure

Each app in `apps/` contains:

```md
---
id: app-name
name: Display Name
category: category
description: Brief description
image: docker/image:tag
ports: [8080]
environment:
  - name: VAR_NAME
    description: What this variable does
    required: false
    default: default-value
volumes:
  - name: data
    description: Data volume
    required: true
    default: ./app/data
---

# App Name

## Description
Longer description of the app.

## Docker Compose
```yaml
services:
  app:
    image: docker/image:tag
    ...
```
```

## Categories

- AI & ML
- Analytics
- Arr Stack
- Cloud Storage
- Container Management
- Database
- Gaming
- Home Automation
- Media Servers
- Monitoring
- Networking
- Productivity
- Security
- Torrents
- VPN

## Contributing

To add a new app:

1. Create `apps/{app-name}.md` with the template structure
2. Add the app to `manifest.json` with id, name, description, category, logo, and defaultPort
3. Test the Docker Compose template manually before submitting

## License

MIT
