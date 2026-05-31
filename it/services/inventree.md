---
title: InvenTree
description: Stock management database for HTL consumables.
published: true
date: 2026-05-31T21:00:00.000Z
tags: it, service, stock, inventory
editor: markdown
dateCreated: 2026-05-31T21:00:00.000Z
---

# InvenTree

Stock management database for HTL consumables (drinks, snacks, materials).

## Service Details

| Property | Value |
|----------|-------|
| **Server** | [HTL Temp Server](/it/servers/htl-temp-server) → will migrate to [Helios](/it/servers/helios) |
| **Port** | 80 |
| **URL** | http://10.72.3.68:80 (HTL network only) |
| **Docs** | [docs.inventree.org](https://docs.inventree.org/) |

## Access

- **URL**: http://10.72.3.68:80
- **Username**: HTL
- **Password**: See [HTL Passwords](/volunteers/htl-passwords)

> Only accessible on the HTL local network.
{.is-warning}

## Usage

InvenTree stores:
- All stock items with categories
- Stock levels and locations
- Prices and barcodes
- Purchase orders

Changes in InvenTree automatically flow to:
- [Stock Frontend](/it/services/stock-frontend) — checkout app
- [Dashboard](/it/services/dashboard) — TV display

## Integration

| System | How |
|--------|-----|
| Stock Frontend | REST API |
| Barcode Scanner | REST API |
| Dashboard | REST API |

## Future Plans

- Move to `*.maakleerplek.be` domain
- Integrate with Authentik SSO
- Move to Soteria infrastructure

## See Also

- [Stock Management System](/volunteers/stock-system) — User guide
- [Stock Frontend](/it/services/stock-frontend)
- [HTL Temp Server](/it/servers/htl-temp-server)
