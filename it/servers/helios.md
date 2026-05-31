---
title: Helios Server
description: Application and storage server for Maakleerplek services.
published: true
date: 2026-05-31T21:00:00.000Z
tags: it, server
editor: markdown
dateCreated: 2026-05-31T21:00:00.000Z
---

# Helios Server

Application and storage server for Maakleerplek. Hosts user-facing services like the stock system, NAS, and other applications. Depends on [Soteria](/it/servers/soteria) for infrastructure (DNS, reverse proxy, SSO).

> **Helios** = Greek god of the sun. This server powers the day-to-day applications.
{.is-info}

## Server Details

| Property | Value |
|----------|-------|
| **Hostname** | helios |
| **Purpose** | Application services & storage |
| **OS** | TBD |
| **IP** | TBD |
| **Location** | TBD |

## Access

```bash
ssh <user>@helios
```

User accounts managed via Ansible — see [User Management](/it/user-management).

## Hosted Services

| Service | Port | Documentation |
|---------|------|---------------|
| NAS | TBD | File storage and backups |
| InvenTree | TBD | [→ InvenTree](/it/services/inventree) |
| Stock Frontend | TBD | [→ Stock Frontend](/it/services/stock-frontend) |
| Dashboard | TBD | [→ Dashboard](/it/services/dashboard) |

> Infrastructure services (DNS, proxy, SSO) run on [Soteria](/it/servers/soteria), not here.
{.is-warning}

## Storage

| Mount | Purpose |
|-------|---------|
| TBD | TBD |

## Backups

TBD — Document backup strategy and NAS configuration.

## See Also

- [Soteria](/it/servers/soteria) — Infrastructure server
- [IT Infrastructure](/it)
- [User Management](/it/user-management)
