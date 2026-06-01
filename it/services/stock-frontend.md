---
title: Stock Frontend
description: React PWA for stock checkout and volunteer management.
published: true
date: 2026-06-01T05:43:23.945Z
tags: 
editor: markdown
dateCreated: 2026-06-01T05:43:23.945Z
---

# Stock Frontend

React/TypeScript PWA for stock checkout and volunteer management.

## Service Details

| Property | Value |
|----------|-------|
| **Server** | [HTL Temp Server](/it/servers/htl-temp-server) → will migrate to [Helios](/it/servers/helios) |
| **Port** | 8086 |
| **URL** | https://10.72.3.68:8086 (HTL network only) |
| **Repository** | [maakleerplek/Stock-management-frontend](https://github.com/maakleerplek/Stock-management-frontend) |

## Modes

### Checkout Mode (Visitor-facing)

1. Visitor scans product barcode
2. Items added to cart with live prices from InvenTree
3. Checkout shows Wero payment QR code
4. Fallback: Payconiq QR on wall

### Volunteer Mode (Password-protected)

Password: See [HTL Passwords](/volunteers/htl-passwords)

Features:
- Add/remove/set stock quantities
- Search items by name, barcode, IPN
- Add new items and categories
- Create and track purchase orders

## Technology

- React + TypeScript
- PWA (installable on devices)
- Connects to InvenTree API

## Future Plans

- Move to `*.maakleerplek.be` domain
- Integrate with Authentik SSO

## See Also

- [Stock Management System](/volunteers/stock-system) — User guide
- [InvenTree](/it/services/inventree)
- [HTL Temp Server](/it/servers/htl-temp-server)