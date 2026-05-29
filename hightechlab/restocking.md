---
title: Restocking
description: How HTL stock gets restocked — drinks, snacks, materials, and who to contact.
published: true
date: 2026-05-15T17:38:11.651Z
tags: htl, stock, restocking, drinks
editor: markdown
dateCreated: 2026-05-07T20:04:05.567Z
---

# Restocking

This page explains how consumable stock (drinks, snacks, materials) gets replenished at the High Tech Lab.

## Fridge Restocking (Volunteer Task)

If an item in the fridge is empty, a **volunteer on duty needs to restock it immediately**. Do not wait for the next order — additional stock is kept in the cellar:

> **Go down to the cellar → turn right → turn right again.** Stock is stored there.
{.is-info}

Grab the needed items and refill the fridge. If the cellar stock is also running low, report it in the HTL WhatsApp group so a new order can be placed.

## Drinks & Snacks

Drinks and snacks are ordered via **[Prik&Tik](https://www.prikentik.be/)**, a Belgian wholesale supplier for community spaces and associations.

Orders are placed by **Ruben Ryckaert**:

| | |
|---|---|
| Email | ruben.ryckaert@maakleerplek.be |
| Phone | +32 468 45 98 66 |

> If drinks are running low or something is missing, **post in the HTL WhatsApp group** and tag or message Ruben directly — don't wait until stock hits zero.
{.is-warning}

The restock threshold for each item is visible in [InvenTree](http://10.72.3.68:80) and the [Stock Management Frontend](https://10.72.3.68:8086) — if current stock is at or below the minimum level shown there, it's time to report it.

## Creating a Purchase Order

When an item is empty or running low, a purchase order should be created in InvenTree to track the restock. This is **internal tracking only** — it does not automatically notify Prik&Tik. You still need to place the order with them directly (phone, webshop, etc.).

**Purchase order workflow:**

| Status | Meaning |
|---|---|
| **Pending** | You're planning to order — not yet placed |
| **Issued** | You've placed the order with Prik&Tik |
| **Received** | Delivery arrived — stock quantities updated automatically |

**To create a purchase order in InvenTree:**

1. Go to [InvenTree](http://10.72.3.68:80) → **Purchasing** → **Purchase Orders** → **New**
2. Select **Prik&Tik** as the supplier
3. Add the items you need (they are pre-linked to Prik&Tik with their pack barcodes)
4. Set quantities in **packs** (drinks = packs of 24, except Stella which is packs of 6)
5. Click **Issue** once you've actually placed the order with Prik&Tik
6. When the delivery arrives, click **Receive** — InvenTree will add the stock automatically

> If you don't have access to InvenTree, **post in the HTL WhatsApp group** and tag Ruben so he can create the order.
{.is-warning}

## Other Materials

Each material category (filament, wood, electronics, etc.) has a responsible volunteer. Find the right person via the **[HTL SharePoint](https://maakleerplek.sharepoint.com/sites/HighTechLab)** or the [Volunteer Contact List](/en/hightechlab/volunteer-contacts). When in doubt, post in the **HTL WhatsApp group** — the relevant person will respond.

## Communication

Volunteers coordinate via **WhatsApp**. There are specific group chats per team and a general HTL group. Use the appropriate group when reporting low stock or issues. If you are not yet in the WhatsApp groups, ask an existing volunteer to add you.

## See Also

- [Stock Prices & Margins](/en/hightechlab/stock-prices) — buying prices, selling prices, and profit margins
- [Stock Management System](/en/hightechlab/stock-system) — how the full stock system works
- [Volunteer Contact List](/en/hightechlab/volunteer-contacts)
