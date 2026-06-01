---
title: IT Infrastructure
description: Overview of Maakleerplek IT infrastructure — servers, services, and user management.
published: true
date: 2026-06-01T05:42:33.795Z
tags: 
editor: markdown
dateCreated: 2026-06-01T05:42:33.795Z
---

# IT Infrastructure

Technical documentation for Maakleerplek's IT systems. This wiki is the source of truth for IT infrastructure — SharePoint's [HTL ICT Info page](https://maakleerplek.sharepoint.com/sites/HighTechLab/SitePages/HTL-ICT-Info-page.aspx) should link here.

> **Access**: To contribute to IT repositories, join the [maakleerplek IT GitHub Team](https://github.com/orgs/maakleerplek/teams/it).
{.is-info}

---

## Architecture Overview

```
┌──────────────────────────────────────────────────────────────────────────┐
│                           MAAKLEERPLEK IT                                │
├──────────────────────────────────────────────────────────────────────────┤
│  INFRASTRUCTURE (Soteria)          │  APPLICATIONS (Helios)              │
│  ┌──────────────────────────────┐  │  ┌──────────────────────────────┐  │
│  │ - DNS                        │  │  │ - NAS / Storage              │  │
│  │ - Nginx Proxy Manager        │  │  │ - InvenTree (stock DB)       │  │
│  │ - Authentik (SSO)            │  │  │ - Stock Frontend             │  │
│  │ - Portainer                  │  │  │ - Dashboard                  │  │
│  │ - Wiki.js                    │  │  │ - Future services...         │  │
│  └──────────────────────────────┘  │  └──────────────────────────────┘  │
├──────────────────────────────────────────────────────────────────────────┤
│  OTHER DEVICES                                                           │
│  ┌─────────────────────┐  ┌─────────────────────────────────────────┐   │
│  │ HTL Temp Server     │  │ Kiosk Pi                                │   │
│  │ (temporary, migrate │  │ (Entrance TV + barcode scanner)         │   │
│  │  to Helios)         │  │                                         │   │
│  └─────────────────────┘  └─────────────────────────────────────────┘   │
├──────────────────────────────────────────────────────────────────────────┤
│  NETWORKING         │  USER MANAGEMENT      │  MICROSOFT 365            │
│  - VLANs            │  - Authentik (SSO)    │  - SharePoint             │
│  - Firewall         │  - Ansible (servers)  │  - Teams                  │
│  - WiFi             │                       │  - Entra ID               │
└──────────────────────────────────────────────────────────────────────────┘
```

---

## Servers

| Server | Purpose | Description | Documentation |
|--------|---------|-------------|---------------|
| **Soteria** | Critical infrastructure | DNS, reverse proxy, SSO, Portainer | [→ Soteria](/it/servers/soteria) |
| **Helios** | Applications & storage | NAS, stock system, user-facing services | [→ Helios](/it/servers/helios) |
| **HTL Temp Server** | Temporary | Currently hosts InvenTree (will migrate to Helios) | [→ HTL Temp Server](/it/servers/htl-temp-server) |
| **Kiosk Pi** | Display | Entrance TV and barcode scanner | [→ Kiosk Pi](/it/servers/kiosk-pi) |

---

## Networking

Network infrastructure — topology, VLANs, DNS, firewall.

[→ Networking](/it/networking)

---

## Services

| Service | Server | Description | Documentation |
|---------|--------|-------------|---------------|
| **Wiki.js** | Soteria | This wiki | [→ Wiki.js](/it/services/wikijs) |
| **Portainer** | Soteria | Docker management GUI | [→ Portainer](/it/services/portainer) |
| **Authentik** | Soteria | SSO identity provider | [→ Authentik](/it/services/authentik) |
| **InvenTree** | HTL Temp Server | Stock database | [→ InvenTree](/it/services/inventree) |
| **Stock Frontend** | HTL Temp Server | Checkout & volunteer app | [→ Stock Frontend](/it/services/stock-frontend) |
| **Dashboard** | Kiosk Pi | Entrance TV display | [→ Dashboard](/it/services/dashboard) |

---

## User Management

| System | Purpose | Documentation |
|--------|---------|---------------|
| **Authentik SSO** | Single sign-on for all web services | [→ User Management](/it/user-management) |
| **Ansible** | Server user accounts and SSH key management | [→ User Management](/it/user-management) |

---

## Microsoft Environment

Microsoft 365 configuration for Maakleerplek — SharePoint, Teams, Entra ID.

[→ Microsoft Environment](/it/microsoft)

---

## Quick Links

- [GitHub: maakleerplek](https://github.com/maakleerplek)
- [Soteria Compose repo](https://github.com/maakleerplek/soteria_compose)
- [Stock Frontend repo](https://github.com/maakleerplek/Stock-management-frontend)
- [Interface-stock repo](https://github.com/maakleerplek/Interface-stock)

---

## Contact

For IT issues: ict@maakleerplek.be or post in the HTL WhatsApp group.