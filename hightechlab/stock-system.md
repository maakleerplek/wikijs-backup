---
title: Stock Management System
description: Overview of the HTL stock system — InvenTree backend, volunteer frontend, TV display, and barcode scanner interface.
published: true
date: 2026-05-15T17:42:21.780Z
tags: htl, stock, inventree, barcode
editor: markdown
dateCreated: 2026-05-07T19:23:59.138Z
---

# Stock Management System

The High Tech Lab uses a barcode-based stock system to manage and sell consumables (drinks, snacks, filament, laser-cutting materials, etc.). The system has four components that work together.

---

## Components

### 1. InvenTree — Stock Database

[InvenTree](https://inventree.org/) is the central stock management platform. It stores all items, categories, stock levels, prices, and barcodes.

- **Instance:** [http://10.72.3.68:80](http://10.72.3.68:80) (HTL network only — temporary, will move to a `*.maakleerplek.be` domain via ICT)
- **Login:** username `HTL`, password in [HTL Passwords](/en/htl-passwords)
- **Docs:** [docs.inventree.org](https://docs.inventree.org/)
- Every item has a unique barcode assigned in InvenTree
- Prices and stock levels are updated here and flow to all other components automatically

---

### 2. Stock Management Frontend — Volunteer & Visitor Web App

A React/TypeScript PWA running at the HTL. It has two modes:

- **App:** [https://10.72.3.68:8086/](https://10.72.3.68:8086/) (HTL network only — temporary, will move to a `*.maakleerplek.be` domain via ICT)
- **GitHub:** [maakleerplek/Stock-management-frontend](https://github.com/maakleerplek/Stock-management-frontend)

#### Checkout Mode (visitor-facing)
The frontend is a website — open it on any device connected to the HTL network.

1. Visitor scans an item's barcode using the **USB barcode scanner** connected to the device
2. Items are added to a shopping cart with live prices from InvenTree
3. At checkout, a **Wero payment QR code** is displayed — visitor scans it in their banking app and pays
4. If Wero doesn't work, **Payconiq** is the fallback — use the **Payconiq QR code on the wall**

#### Volunteer Mode (password-protected)
Volunteer mode is accessible directly from the stock frontend — there is a button on the main screen to switch to it. Enter the password from [HTL Passwords](/en/htl-passwords) to unlock.

Once in volunteer mode you have full control over the stock:
- Add stock, remove stock, or set exact quantities
- Search items by name, barcode, or IPN
- Add new items or categories to InvenTree directly from the interface
- Create and track **purchase orders** under the "Purchase Orders" tab

> **Item empty or running low?** Go to the **Purchase Orders** tab in volunteer mode and create a purchase order. Then place the order with the supplier (e.g. Prik&Tik) and mark it as issued. When the delivery arrives, receive it in InvenTree to update stock automatically.
> → Full instructions: **[Restocking](/en/hightechlab/restocking)**
{.is-warning}

---

### 3. TV Presentation — Info Screen

A Next.js dashboard running on the entrance TV (via a Raspberry Pi kiosk). See → [Info Screen — Raspberry Pi Kiosk](/en/ict/infra/kiosk-screen).

- Shows **live stock levels** for drinks, snacks, and materials pulled from InvenTree
- Shows machine usage prices, upcoming events, weather, and news
- Updates automatically every 15 minutes — stock changes won't appear immediately
- Also displays a **payment QR code** in the inventory panel so visitors can pay without going through the checkout flow

---

### 4. Interface-stock — Physical Barcode Scanner (LCD)

A Python script running on a Raspberry Pi (4B or 5, Bookworm) with a Waveshare 2.4" LCD touchscreen. **Located next to the TV** at the HTL entrance.

![Interface-stock CAD design](/u/interface-stock-cad.png =250x){.align-right}

- **GitHub:** [maakleerplek/Interface-stock](https://github.com/maakleerplek/Interface-stock)
- **OnShape:** [3D design](https://cad.onshape.com/documents/t/69c57f84c4bc5ed2b8ffc598)

**Shopping flow:**
1. Scan a product barcode → item appears on screen with image and price
2. Scan the same barcode again → quantity increments
3. Scan the **CONFIRM barcode** (first time) → shows order summary and total
4. Scan **CONFIRM** again → displays a **Wero payment QR code** with the total amount
5. Scan **CONFIRM** a third time → cart clears, ready for next customer

The **CONFIRM barcode** is a physical barcode card with the text `CONFIRM` — keep it next to the scanner. The payment description includes item categories (e.g. `HTL Makerspace - drink - wood`) so purchases are identifiable in bank statements.

Runs as `inventree-scanner.service` and starts automatically on boot.

**Service commands:**
```bash
sudo systemctl restart inventree-scanner.service   # after code updates
sudo systemctl status inventree-scanner.service    # check if running
sudo journalctl -u inventree-scanner.service -f    # live logs
```

**Updating the code:**
```bash
git pull
source .venv/bin/activate && pip install -r requirements.txt
sudo systemctl restart inventree-scanner.service
```

**Setup / `.env` config** (needed if rebuilding):

| Variable | Value |
|---|---|
| `INVENTREE_URL` | `http://10.72.3.68:80` |
| `INVENTREE_TOKEN` | see [HTL Passwords](/en/htl-passwords) |
| `VITE_PAYMENT_NAME` | `Hightechlab/Maakleerplek` |
| `VITE_PAYMENT_IBAN` | see [HTL Passwords](/en/htl-passwords) |
| `HTL_NAME` | `HTL Makerspace` |
| `HTL_CODE` | `HTL001` |

Run `./install.sh` for full setup (installs deps, configures SPI, registers the service).

**Hardware — Waveshare 2.4" LCD (SPI)**

![Waveshare 2.4" LCD specs](/u/interface-stock-waveshare-specs.png =400x)

![Raspberry Pi wiring diagram](/u/interface-stock-wiring.png =400x)

---

## Barcode Workflow (end to end)

```
InvenTree (item + barcode defined)
        │
        ▼
   Visitor scans barcode
        │
   ┌────┴────────────────────────┐
   │ Web frontend                │ Physical LCD scanner
   │ (checkout mode)             │ (Interface-stock)
   └────┬────────────────────────┘
        │
        ▼
   Shopping cart (live prices from InvenTree)
        │
        ▼
   Payment QR code (Wero / Payconiq)
        │
        ▼
   Visitor pays via banking app
```

---

## Payment

All payments are cashless:

- **Primary:** [Wero](https://www.wero.be/) — QR code generated on the spot from the cart total in the frontend or LCD scanner
- **Fallback:** Payconiq — fixed QR code on the wall for manual payment if Wero fails

No cash handling. If a visitor can't pay digitally, ask them to sort it out with a volunteer or come back.

---

## Contributing

As a volunteer, you can help improve the stock system. The code lives on GitHub:

- [maakleerplek/Stock-management-frontend](https://github.com/maakleerplek/Stock-management-frontend)
- [maakleerplek/Interface-stock](https://github.com/maakleerplek/Interface-stock)

To get access, request to join the [maakleerplek GitHub team](https://github.com/maakleerplek) or message one of the **admins listed in the GitHub repository** (check the README or the team page). Once added you can contribute via pull requests.

---

## See Also

- [Prices](/en/hightechlab/prices) — public price list
- [Stock Prices & Margins](/en/hightechlab/stock-prices) — internal buying prices and profit margins
- [Restocking](/en/hightechlab/restocking) — how and when to reorder drinks and materials
- [Info Screen — Raspberry Pi Kiosk](/en/ict/infra/kiosk-screen) — TV display setup
- [Temporary HTL Server](/en/ict/infra/htl-temp-server) — server hosting InvenTree and the frontend
- [HTL Passwords](/en/htl-passwords) — volunteer mode password and other credentials
- [InvenTree documentation](https://docs.inventree.org/)
