---
title: Portainer
description: Docker container management GUI.
published: true
date: 2026-06-01T05:43:11.418Z
tags: 
editor: markdown
dateCreated: 2026-06-01T05:43:11.418Z
---

# Portainer

Docker container management GUI for Soteria.

## Service Details

| Property | Value |
|----------|-------|
| **Server** | [Soteria](/it/servers/soteria) |
| **Port** | 9000 |
| **URL** | http://soteria.maakleerplek.be:9000 |
| **Compose file** | `infrastructure/compose.yml` |

## Access

Login with your Portainer account. Request access from IT team.

## Usage

### Deploying Stacks

1. Go to **Stacks**
2. Click existing stack or **Add stack**
3. For Git-based stacks:
   - Repository URL: `https://github.com/maakleerplek/soteria_compose`
   - Compose path: `docker-compose.yml`
   - Upload environment variables from `secrets/.env`
4. Click **Deploy** or **Pull and redeploy**

### Viewing Logs

1. Go to **Containers**
2. Click the container name
3. Click **Logs**

### Restarting Services

1. Go to **Containers**
2. Select containers
3. Click **Restart**

## Data

Portainer data is stored in `/docker_data/portainer/` and backed up to NAS.

## See Also

- [Soteria Server](/it/servers/soteria)
- [Soteria Documentation](/it/soteria-doc)