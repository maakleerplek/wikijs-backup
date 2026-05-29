---
title: Temporary HTL Server
description: Temporary HTL server — a laptop running Ubuntu Server hosting the InvenTree backend and stock management frontend.
published: true
date: 2026-05-12T14:04:57.056Z
tags: htl, ict, server, infrastructure
editor: markdown
dateCreated: 2026-05-07T20:04:00.288Z
---

# Temporary HTL Server

The current HTL server is a **laptop running Ubuntu Server**. It hosts the InvenTree stock database, the stock management frontend, and other HTL services. This is a temporary setup — it will be migrated to proper infrastructure with `*.maakleerplek.be` domains by the ICT team.

## Access

```
ssh htl-tempserver@10.72.3.68
```

Password: see [HTL Passwords](/en/htl-passwords) (guest)

> Only accessible on the HTL local network.
{.is-warning}

## Hosted Services

| Service | Address | Notes |
|---|---|---|
| InvenTree (stock database) | [http://10.72.3.68:80](http://10.72.3.68:80) | Login: HTL / see passwords |
| Stock Management Frontend | [https://10.72.3.68:8086](https://10.72.3.68:8086) | Volunteer & checkout app |

## Maintainers

Maintainers are listed in the relevant **GitHub repositories** under the [maakleerplek](https://github.com/maakleerplek) organisation. For urgent issues, post in the HTL WhatsApp group.

## See Also

- [HTL Passwords](/en/htl-passwords)
- [Stock Management System](/en/hightechlab/stock-system)
- [Info Screen — Raspberry Pi Kiosk](/en/ict/infra/kiosk-screen)
