# Wagmios Marketplace

> Pre-configured Docker Compose templates for self-hosted apps.

**Browse the live marketplace:** https://mentholmike.github.io/marketplace

---

## Overview

This marketplace contains Docker Compose templates for 35+ popular self-hosted applications. Each app is defined as a simple markdown file that AI agents can read to install services on your server.

**Powered by [Wagmios](https://github.com/mentholmike/wagmios)** — a Docker container management dashboard with AI agent support.

---

## Browse Apps

The marketplace is live at **https://mentholmike.github.io/marketplace**

Browse by category, search for apps, and click any card to view the full Docker Compose template on GitHub.

---

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

---

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

---

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
- Notifications
- Photo & Video
- Productivity
- Search
- Security
- Torrents
- Utilities
- VPN

---

## Contributing

To add a new app:

1. Create `apps/{app-name}.md` with the template structure
2. Add the app to `manifest.json` with id, name, description, category, logo, and defaultPort
3. Test the Docker Compose template manually before submitting

---

## License

MIT
