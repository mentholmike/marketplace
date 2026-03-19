---
id: supabase
name: Supabase
category: database
description: Self-hosted Firebase alternative. Database, auth, storage, and real-time APIs for your apps.
image: supabase/postgres:15.1.0.147
ports: [5432, 54321]
environment:
  - name: POSTGRES_PASSWORD
    description: PostgreSQL password
    required: true
  - name: ANON_KEY
    description: Public anon key
    required: false
  - name: SERVICE_KEY
    description: Service role key
    required: false
  - name: TZ
    description: Timezone
    required: false
    default: UTC
volumes:
  - name: db-data
    description: PostgreSQL data directory
    required: true
    default: ./supabase/db
---

# Supabase

## Description
Supabase is an open source Firebase alternative. Self-host a complete backend with PostgreSQL database, authentication, file storage, and real-time subscriptions.

## Ports
- **5432** — PostgreSQL database
- **54321** — Supabase Studio (admin UI)

## Environment Variables
| Variable | Required | Default | Description |
|----------|----------|---------|-------------|
| `POSTGRES_PASSWORD` | Yes | — | PostgreSQL password |
| `ANON_KEY` | No | — | Public anon key for client apps |
| `SERVICE_KEY` | No | — | Service role key for admin |
| `TZ` | No | UTC | Timezone |

## Volumes
| Volume | Description |
|--------|-------------|
| `db-data` | PostgreSQL data directory |

## Docker Compose
```yaml
services:
  postgres:
    image: supabase/postgres:15.1.0.147
    container_name: supabase-postgres
    ports:
      - "5432:5432"
    environment:
      - POSTGRES_PASSWORD=${POSTGRES_PASSWORD}
      - POSTGRES_HOST_AUTH_METHOD=trust
    volumes:
      - ./supabase/db:/var/lib/postgresql/data
    restart: unless-stopped

  studio:
    image: supabase/studio:latest
    container_name: supabase-studio
    ports:
      - "54321:3000"
    environment:
      - STUDIO_PG_META_URL=http://meta:8080
      - POSTGRES_PASSWORD=${POSTGRES_PASSWORD}
    restart: unless-stopped

  meta:
    image: supabase/postgres-meta:latest
    container_name: supabase-meta
    ports:
      - "8080:8080"
    environment:
      - PG_META_PORT=8080
      - PG_META_DB_HOST=postgres
      - PG_META_DB_PASSWORD=${POSTGRES_PASSWORD}
    restart: unless-stopped
```

## Notes
- Access Supabase Studio at `http://your-server:54321`
- Connect your app using the PostgreSQL connection string: `postgresql://postgres:${POSTGRES_PASSWORD}@your-server:5432`
- For full Supabase (auth, storage, realtime), see supabase/self-host for Kubernetes deployment
- This is a minimal setup focused on the database — for production consider the full Kubernetes deployment
