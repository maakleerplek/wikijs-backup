---
title: Wiki.js
description: Wiki.js service configuration and management.
published: true
date: 2026-05-31T21:00:00.000Z
tags: it, service, wiki
editor: markdown
dateCreated: 2026-05-31T21:00:00.000Z
---

# Wiki.js

This wiki — documentation platform for Maakleerplek.

## Service Details

| Property | Value |
|----------|-------|
| **Server** | [Soteria](/it/servers/soteria) |
| **Port** | 3081 |
| **URL** | https://wiki.maakleerplek.be |
| **Stack** | Wiki.js + PostgreSQL |
| **Compose file** | `services/wikijs-wiki-prod-sot/compose.yml` |

## Access

- **Public**: https://wiki.maakleerplek.be
- **Admin**: Login required (Authentik SSO planned)

## Configuration

### Environment Variables

| Variable | Description |
|----------|-------------|
| `POSTGRES_DB` | Database name |
| `POSTGRES_USER` | Database user |
| `POSTGRES_PASSWORD` | Database password |

Secrets stored in `./secrets/.env` on Soteria.

### Data

| Type | Location |
|------|----------|
| Database | `/var/lib/docker/volumes/wikijs-wiki-prod-sot_wikidb-data/_data` |
| Git sync | This repository (wikijs-backup) |

## Backup

Wiki content is synced to Git automatically. Database is backed up with the `/docker_data/` backup to NAS.

## See Also

- [Soteria Server](/it/servers/soteria)
- [Soteria Documentation](/it/soteria-doc)
