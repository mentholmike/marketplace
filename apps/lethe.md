---
id: lethe
name: Lethe
category: AI & ML
description: Persistent memory layer for AI agents. Gives your agent long-term memory across sessions.
image: ghcr.io/openlethe/lethe:latest
ports: ["18483:18483"]
environment:
  - name: LETHE_API
    description: Optional API key for authentication
    required: false
  - name: RUST_LOG
    default: info
volumes:
  - name: lethe-data
    description: Lethe SQLite database and data
    required: true
    default: ./lethe/data
---

# Lethe

## Description
Lethe is a persistent memory layer for AI agents. Every decision, observation, task, and flag persists across sessions and survives container restarts.

Works with OpenClaw agents. The agent accumulates knowledge and maintains continuity between sessions.

## Ports
- **18483** — Lethe HTTP API

## Environment Variables
| Variable | Required | Default | Description |
|----------|----------|---------|-------------|
| `LETHE_API` | No | — | Optional API key authentication |
| `RUST_LOG` | No | info | Log level (debug, info, warn, error) |

## Volumes
| Volume | Description |
|--------|-------------|
| `lethe-data` | SQLite database and persistent data |
