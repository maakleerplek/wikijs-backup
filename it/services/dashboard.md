---
title: Dashboard
description: Entrance TV dashboard showing events and stock.
published: true
date: 2026-05-31T21:00:00.000Z
tags: it, service, dashboard, kiosk
editor: markdown
dateCreated: 2026-05-31T21:00:00.000Z
---

# Dashboard

Full-screen Next.js dashboard displayed on the HTL entrance TV.

## Service Details

| Property | Value |
|----------|-------|
| **Server** | [HTL Temp Server](/it/servers/htl-temp-server) |
| **Display** | [Kiosk Pi](/it/servers/kiosk-pi) |
| **Port** | 8083 |
| **URL** | http://10.72.3.68:8083 |

## Layout

The dashboard is divided into three columns:

### Left — Context Panel
- Current time and date
- Live weather from Open-Meteo
- Next workshop with registration QR

### Centre — Event Carousel
- Upcoming workshops and events from MaakLeerPlek WordPress
- Event image, title, date/time, description
- QR code to event page
- News articles from `/verhalen/`

### Right — Inventory Panel
- Live stock levels from InvenTree
- Item names, counts, prices
- Payment QR code
- Recent purchase activity feed

### Footer
- QR codes to maakleerplek.be and wiki
- HTL logo and version

## Data Sources

| Data | Source | Refresh |
|------|--------|---------|
| Events | WordPress REST API | Carousel rotation |
| Weather | Open-Meteo API | Periodic |
| Stock | InvenTree API | 5 minutes |
| Purchases | POST /api/changelog | Real-time |

## See Also

- [Kiosk Pi](/it/servers/kiosk-pi) — Hardware and CEC control
- [Stock Management System](/volunteers/stock-system)
